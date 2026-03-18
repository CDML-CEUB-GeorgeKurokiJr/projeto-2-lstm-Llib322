Linha do Tempo da Pesquisa: A Evolução do Modelo Preditivo (MSFT)
Este documento narra a ordem cronológica dos experimentos realizados na arquitetura de rede neural para a previsão das ações da Microsoft. Cada teste foi desenhado para isolar variáveis e compreender o comportamento matemático do mercado financeiro.

Fase 1: Os Primeiros Passos e o Teste de Ruído
Teste 1: O Modelo Base (Baseline Inicial)

O que fizemos: Criamos uma arquitetura simples (LSTM + GRU) usando apenas os dados básicos de mercado, prevendo com uma janela de 60 dias. Treinamos um ensemble de 100 redes.

Resultado: MAPE de 2.24% | MAE: US$ 10.29

Conclusão: O modelo demonstrou capacidade de aprendizado, mas ainda estava muito vulnerável às oscilações bruscas.

<img width="1160" height="547" alt="image" src="https://github.com/user-attachments/assets/229bedf2-a860-41d1-9bdf-88a02d537291" />

Teste 2: A Hipótese da Pandemia (Cisne Negro)

O que fizemos: Removemos os dados caóticos do ano de 2020 para testar se a anomalia da pandemia estava "confundindo" a inteligência artificial.

Resultado: MAPE piorou para 3.68% | MAE: US$ 18.55

Conclusão: Refutamos a hipótese. A piora drástica provou que a IA precisa ver crises passadas para aprender a lidar com a volatilidade do futuro. Retornamos os dados de 2020 para a base.

<img width="1160" height="547" alt="image" src="https://github.com/user-attachments/assets/538d4eac-99d9-4639-a9ae-47f2179d5a13" />

Fase 2: A Engenharia de Dados (O Ponto de Virada)
Teste 3: O "Megazord" de 17 Features

O que fizemos: Enriquecemos drasticamente o contexto da IA. Adicionamos indicadores técnicos (MACD, RSI, Bandas de Bollinger) e variáveis macroeconômicas (S&P 500 e VIX), totalizando 17 colunas.

Resultado: MAPE caiu para 1.81% | MAE: US$ 8.34

Conclusão: Salto gigantesco de performance. Provou-se que contexto financeiro importa mais do que apenas olhar para o preço isolado da ação.

<img width="1160" height="548" alt="image" src="https://github.com/user-attachments/assets/0acb2747-280c-4485-80cb-4e75f844b40a" />

Fase 3: O Estudo de Ablação (Testando a Complexidade)
Teste 4: O Paradoxo do Over-engineering

O que fizemos: Aplicamos técnicas de Estado da Arte (Mecanismo de Atenção + Bi-LSTM + Dropout) simultaneamente no modelo de 17 variáveis.

Resultado: MAPE despencou para 4.35% | MAE: US$ 20.00

Conclusão: O modelo sofreu over-smoothing (suavização excessiva). A camada de Atenção transformou a rede em uma média móvel preguiçosa. Decidimos desmontar o modelo e testar os recursos um a um.

<img width="1160" height="547" alt="image" src="https://github.com/user-attachments/assets/281b4f65-fe73-4311-8983-85bc04dc1a97" />

Teste 5: Baseline + Otimização Bayesiana (Optuna)

O que fizemos: Voltamos para o modelo simples (sem atenção e sem dropout) e usamos o Optuna para encontrar a quantidade perfeita de neurônios e a taxa de aprendizado ideal.

Resultado: MAPE excelente de 1.46% | MAE: US$ 6.70

Conclusão: A otimização dos hiperparâmetros era a peça que faltava para afinar o modelo simples.

<img width="1160" height="548" alt="image" src="https://github.com/user-attachments/assets/0267c217-6604-42d3-98da-f53f09a48427" />

Teste 6: Teste Isolado da Bi-LSTM

O que fizemos: Mantivemos os parâmetros otimizados e adicionamos APENAS a funcionalidade bidirecional (Bi-LSTM).

Resultado: MAPE melhorou para 1.38% | MAE: US$ 6.26

Conclusão: Isolada, a Bi-LSTM provou ser superior à LSTM comum, lendo o contexto temporal em duas direções com maestria.

<img width="1160" height="548" alt="image" src="https://github.com/user-attachments/assets/5ea48615-4e13-4f11-bc51-4c82e6821686" />

Teste 7: Teste Isolado do Dropout (Amnésia)

O que fizemos: Adicionamos uma taxa de esquecimento de 10% (Dropout) à nossa nova campeã (Bi-LSTM) para tentar evitar overfitting.

Resultado: MAPE piorou para 1.69% | MAE: US$ 7.80

Conclusão: O mercado financeiro é ruidoso. Desligar neurônios causou underfitting. A rede precisa de potência máxima. Dropout foi descartado.

<img width="1160" height="548" alt="image" src="https://github.com/user-attachments/assets/e8183ee7-172c-4077-ac3d-5aee2d963e7c" />

Fase 4: O Domínio do Tempo
Teste 8: Encurtando a Memória (Janela de 20 Dias)

O que fizemos: Questionamos a janela padrão de 60 dias úteis e reduzimos para 20 dias (1 mês).

Resultado: MAPE caiu para 1.30% | MAE: US$ 5.85

Conclusão: A Microsoft possui movimentos rápidos. Descartar informações velhas diminuiu a confusão do modelo.

<img width="1160" height="547" alt="image" src="https://github.com/user-attachments/assets/99646ace-32e8-48f6-b86c-fc0fa3e34b9d" />

Teste 9: A Busca em Grade Temporal (Grid Search)

O que fizemos: Rodamos testes curtos em várias janelas de tempo (10, 15, 20, 25, 30 e 45 dias) para encontrar o ponto matemático perfeito.

Resultado do Ranking: A janela de 30 dias venceu (MAPE de 1.27% nesses testes curtos).

Conclusão: 1 mês e meio de histórico é o equilíbrio exato entre entender a tendência e evitar ruído.

Fase 5: O Modelo Definitivo
Teste 10: O Teste de Sanidade (100 Redes)

O que fizemos: Rodamos o modelo completo (Janela de 30 dias + Bi-LSTM pura) com os novos hiperparâmetros massivos descobertos por uma bateria de 500 testes do Optuna (LSTM 128, GRU 144). Treinamos 100 redes.

Resultado: MAPE de 1.30% | MAE: US$ 5.81

Conclusão: Atingimos o Noise Floor (piso de ruído) do mercado. A rede é hiper-estável.

<img width="1160" height="547" alt="image" src="https://github.com/user-attachments/assets/9b4588cf-5ce2-49d8-afc4-eeb0362d4bc8" />

Teste 11: O Experimento Absoluto (2.000 Redes)

O que fizemos: Para extrair o limite físico da previsibilidade e anular completamente qualquer aleatoriedade, rodamos um ensemble massivo de 2.000 redes neurais.

Resultado Final Oficial: MAPE de 1.27% | MAE: US$ 5.73

Conclusão: O modelo final é uma prova matemática de robustez, apresentando um erro irrisório para um ativo de alta volatilidade financeira.

<img width="1160" height="547" alt="image" src="https://github.com/user-attachments/assets/83196062-97f2-479c-bdf6-72b6d4588eda" />
