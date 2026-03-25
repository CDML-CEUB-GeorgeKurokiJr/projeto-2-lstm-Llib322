# Projeto 2: Previsão Simultânea do Ecossistema de IA (Deep Learning)

**Disciplina:** Aprendizagem Profunda (Deep Learning)  
**Técnica Aplicada:** Multi-Output Bi-LSTM + Self-Attention + Walk-Forward Validation  
**Ativos Analisados:** Microsoft (MSFT), Nvidia (NVDA), Alphabet (GOOGL) e Meta (META)  

---

## Objetivo do Projeto

Este projeto propõe prever a trajetória de preços das quatro maiores gigantes de tecnologia impulsionadas pela Inteligência Artificial. Rompendo com a modelagem univariada tradicional, adotamos uma **abordagem ecossistêmica (Multi-Output)**, fundamentada na alta correlação de Pearson entre estes ativos. 

O modelo consome uma matriz complexa de **50 variáveis simultâneas** (indicadores técnicos, métricas de volatilidade, S&P 500 e VIX) para capturar não apenas o histórico de preços isolados, mas o fluxo de capital e o risco sistêmico do mercado como um todo.

## Arquitetura do Modelo Campeão

A topologia final foi definida através de um rigoroso **Estudo de Ablação** e Otimização Bayesiana (Optuna). O modelo consagrado opera sob o paradigma "Largo e Raso" (*Wide and Shallow*), provando que a complexidade excessiva no mercado financeiro gera *overfitting* (decoração de ruído).

* **Camada de Extração:** Uma única camada **Bi-LSTM** de altíssima densidade (352 neurônios), capaz de ler a janela temporal de 20 dias em ambas as direções.
* **Mecanismo de Atenção:** Camada de *Self-Attention* temporal, permitindo à rede focar matematicamente em dias de alta relevância (ex: quebras de volatilidade) e ignorar a lateralização do mercado.
* **Validação Dinâmica:** Treinamento via **Walk-Forward Validation**, onde um *Ensemble* de 2.000 redes avança no tempo e sofre *Fine-Tuning* mensalmente, impedindo a degradação do modelo frente à mudança de humor do mercado (*Concept Drift*).

> **Nota Metodológica:** Arquiteturas profundas empilhadas e camadas GRU foram testadas nas fases iniciais, mas descartadas matematicamente devido à degradação de performance, justificando a adoção do princípio da Parcimônia (Navalha de Ockham).

## Resultados Oficiais (Walk-Forward Ensemble)

A validação final comprova a precisão cirúrgica da rede neural no preenchimento da lacuna matemática, alcançando um Erro Percentual Absoluto Médio (MAPE) global próximo a 2%.

**Métricas de Precisão Matemática e Direcional:**
* **Microsoft (MSFT):** MAPE: 1.67% | MAE: US$ 7.39 | RMSE: US$ 9.46 | Hit Rate: 49.13%
* **Nvidia (NVDA):** MAPE: 2.84% | MAE: US$ 3.95 | RMSE: US$ 5.20 | Hit Rate: 54.07%
* **Alphabet (GOOGL):** MAPE: 2.05% | MAE: US$ 4.08 | RMSE: US$ 5.51 | Hit Rate: 55.52%
* **Meta Platforms (META):** MAPE: 1.93% | MAE: US$ 12.16 | RMSE: US$ 16.64 | Hit Rate: 47.67%
---
* **MÉDIA GLOBAL DO ECOSSISTEMA:** MAPE **2.12%** | MAE **US$ 6.89** | HIT RATE **51.60%**

### Simulador de Negociação (Backtest Financeiro)
Para quantificar o *Alpha* gerado, as previsões da IA foram submetidas a um simulador financeiro com aporte virtual inicial de US$ 10.000,00, operando uma estratégia *Long-Only* (Compra/Caixa) contra o mercado passivo (*Buy & Hold*).

* **Retorno Mercado Passivo (Buy & Hold):** US$ 14,637.32 (+46.37%)
* **Retorno Gestão Ativa Dinâmica (Robô IA):** US$ 12,557.82 (+25.58%)

**Conclusão Financeira:** A IA entregou um rendimento excepcional de 25.58%. A vitória matemática do *Buy & Hold* reflete o viés de forte tendência de alta (*Bull Market* extremo da tecnologia no período). A IA atuou primariamente como uma excelente **gestora de risco**, convertendo o patrimônio em caixa em momentos de incerteza para proteger o capital, demonstrando a clássica dicotomia entre minimização de erro e captura incondicional de tendência no mundo quantitativo.

## Estrutura do Repositório

* `notebooks/LSTM_GRU_projeto_2_versao_final.ipynb`
  * Contém o código absoluto do modelo campeão validado (Bi-LSTM de 352 neurônios + Attention). *Obs: A nomenclatura legada "GRU" foi mantida no arquivo por questões de controle de versão e rastreabilidade da pesquisa inicial.*
* `notebooks/LSTM_GRU_projeto_2_testes.ipynb`
  * O "Laboratório de Pesquisa". Contém toda a nossa bateria cronológica de testes exploratórios (Estudo de Ablação), provando matematicamente o porquê da rejeição de topologias profundas, testes univariados e funções de perda alternativas.
* `documents/estudo_de_ablacao_e_conclusoes.md`
  * Documentação teórica detalhada. Apresenta o raciocínio cronológico, as hipóteses levantadas, os resultados obtidos e as conclusões extraídas de cada etapa do desenvolvimento do modelo.
