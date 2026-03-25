# Diário de Pesquisa Quantitativa: Estudo de Ablação e Evolução Arquitetural

**Projeto:** Previsão Simultânea do Ecossistema de IA (Multi-Output)
**Objetivo do Documento:** Registrar cronologicamente as hipóteses testadas, os resultados empíricos obtidos e as decisões arquiteturais tomadas durante o desenvolvimento do modelo preditivo de Deep Learning.

---

## Fase 1: Análise Exploratória e Validação da Abordagem Multivariada
**Hipótese:** Empresas líderes no desenvolvimento de Inteligência Artificial (Microsoft, Nvidia, Alphabet e Meta) não operam em um vácuo financeiro; elas formam um ecossistema com forte co-movimento. Analisá-las isoladamente (modelos univariados) descartaria informações valiosas.
**Metodologia:** Cálculo da Matriz de Correlação de Pearson entre os retornos dos ativos.
**Resultado:** Identificamos correlações estatisticamente relevantes (frequentemente superiores a 0.55).
**Conclusão Arquitetural:** A hipótese foi validada. Justifica-se a transição para uma arquitetura Multi-Output, onde uma única rede neural prevê a trajetória dos quatro ativos simultaneamente, aprendendo com o fluxo de capital sistêmico.

---

## Fase 2: A Maldição da Profundidade (Redes Empilhadas vs. Wide & Shallow)
**Hipótese:** O aumento da complexidade da rede neural (adição de camadas profundas, como o empilhamento de Bi-LSTM com GRU) permitiria ao modelo abstrair padrões não-lineares mais complexos a partir das 50 variáveis de entrada.
**Metodologia:** Treinamento de arquiteturas Stacked RNN e comparação com arquiteturas de camada única, avaliadas por otimização Bayesiana (Optuna).
**Resultado:** O modelo profundo sofreu severa degradação de performance (aumento expressivo do RMSE). A rede começou a decorar o ruído das 50 variáveis (Overfitting).
**Conclusão Arquitetural:** O mercado financeiro possui uma relação Sinal/Ruído excessivamente baixa. Comprovamos o princípio da Parcimônia: a otimização elegeu uma arquitetura "Larga e Rasa" (uma única camada Bi-LSTM de 352 neurônios) como a topologia ideal, possuindo o balanço perfeito entre capacidade cognitiva e generalização. A camada GRU e camadas adicionais foram definitivamente descartadas.

---

## Fase 3: Mitigação de Ruído Temporal (Mecanismo de Atenção)
**Hipótese:** A janela histórica de 20 dias não possui peso linear. Eventos específicos (como quebras de volatilidade ou balanços trimestrais) ditam a tendência futura com mais força do que dias de lateralização.
**Metodologia:** Implementação de uma camada de Self-Attention (Atenção Cruzada) logo após a saída dos estados ocultos da Bi-LSTM.
**Resultado:** Aumento da estabilidade preditiva e redução de outliers nos erros de previsão.
**Conclusão Arquitetural:** A camada de Atenção foi efetivada no modelo final. Ela permitiu à rede criar uma distribuição de probabilidade (Softmax) sobre a janela de 20 dias, forçando o modelo a focar matematicamente nos dias de maior relevância informacional.

---

## Fase 4: O Teste de Trajetória (Multi-Step Forecast t+5)
**Hipótese:** Obrigar a rede neural a prever a trajetória de 5 dias no futuro provaria que ela abstraiu a tendência macro, em vez de apenas replicar ingenuamente o preço do dia anterior (Naive Forecast).
**Metodologia:** Alteração da camada linear de saída para prever 20 valores simultâneos (5 dias no futuro para os 4 ativos).
**Resultado:** O Erro Percentual Absoluto Médio (MAPE) do Dia 1, que estava estabilizado na faixa de 2.50%, saltou para mais de 6.20%.
**Conclusão Arquitetural:** Ocorreu a "Diluição do Foco Matemático". Ao forçar a rede a prever o futuro distante, ela sacrificou a precisão do curto prazo para minimizar o erro global. Retornamos à arquitetura de passo único (Day-Ahead, t+1), comprovando que modelos de alta precisão em finanças atuam melhor sob foco temporal estrito.

---

## Fase 5: Função de Perda Híbrida (Penalidade Direcional)
**Hipótese:** O Erro Quadrático Médio (MSE) é direcionalmente cego. Se aplicarmos uma Função de Perda Customizada que multiplique o erro da rede por 3x sempre que ela errar a direção do mercado (Hit Rate), a IA aprenderá a priorizar o acerto da tendência.
**Metodologia:** Substituição da função `nn.MSELoss` por uma Loss Híbrida direcional.
**Resultado:** O Hit Rate (Acurácia Direcional) global subiu para a faixa de 52.50% (com picos de 56% na Alphabet), mas o Erro Absoluto em dólares (MAE) explodiu.
**Conclusão Arquitetural:** A rede desenvolveu "aversão ao erro direcional", porém o custo (Trade-off) foi a perda da precisão cirúrgica no preço exato. Como o escopo do projeto exige regressão de alta precisão de valor, a Loss Híbrida foi rejeitada e a função MSE clássica foi restaurada.

---

## Fase 6: O Paradigma Dinâmico (Walk-Forward Validation)
**Hipótese:** O modelo estático sofre de Deriva de Conceito (Concept Drift). Um modelo treinado em 2023 não pode prever 2025 com precisão sem atualizar sua matriz de pesos, devido à não-estacionariedade do mercado.
**Metodologia:** Simulação de Janela Expansiva. A rede é re-treinada (Fine-Tuning de 3 épocas) a cada bloco de 20 dias úteis durante o avanço pelo período de teste.
**Resultado:** Queda drástica no erro preditivo. O MAPE global atingiu excelentes 2.12%, com a Microsoft cravando 1.67% e a Meta 1.93%.
**Conclusão Arquitetural:** Validou-se que a contínua atualização dos pesos da rede é mandatória no mercado quantitativo. O Walk-Forward Validation foi integrado como o motor oficial do modelo definitivo.

---

## Fase 7: Backtest Financeiro (A Prova de Fogo)
**Hipótese:** Um modelo com 2.12% de erro de preço é intrinsecamente capaz de gerar lucros (Alpha) superiores ao mercado passivo.
**Metodologia:** Simulação quantitativa operando um capital virtual de US$ 10.000,00 com regra Long-Only (Sinal de Compra vs. Sinal de Caixa/Proteção), confrontada contra a estratégia Buy & Hold.
**Resultado Empírico:**
- Rentabilidade Buy & Hold: +46.37% (Absorção total de risco)
- Rentabilidade IA: +25.58% (Gestão dinâmica)
**Conclusão Final:** O teste refutou a hipótese inicial e evidenciou uma premissa madura de Wall Street: prever o preço não garante bater o mercado direcional. A IA atuou como uma rigorosa gestora de risco, limitando as perdas, mas abdicando de saltos irracionais do mercado. O resultado de 25.58% é excepcional no mundo real, atestando a validade do algoritmo como ferramenta de suporte à decisão, embora confirme a dificuldade matemática de superar estratégias passivas durante *Bull Markets* agressivos no setor de tecnologia.
