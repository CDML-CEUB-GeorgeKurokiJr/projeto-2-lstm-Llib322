# Registro Oficial de Testes e Resultados de Ablação

**Projeto:** Previsão Simultânea do Ecossistema de Inteligência Artificial  
**Natureza do Documento:** Logbook de validação empírica. Contém os recortes literais das saídas de terminal geradas durante a execução cronológica dos scripts de teste.

---

## 1.1. Refinamento do Ecossistema: O Quarteto Big Tech (MSFT, GOOGL, NVDA, META)
**Objetivo:** Provar matematicamente a interdependência e o co-movimento dos ativos selecionados, justificando o uso de uma arquitetura preditiva de múltiplas saídas (Multi-Output).  
**Método:** Cálculo estático da Matriz de Correlação de Pearson ($r$).  
**Resultado Literal:**
```text
Matriz de Correlação Matemática (Quarteto):
Ticker     GOOGL      META      MSFT      NVDA
Ticker                                        
GOOGL   1.000000  0.608215  0.695322  0.566107
META    0.608215  1.000000  0.617550  0.527913
MSFT    0.695322  0.617550  1.000000  0.666643
NVDA    0.566107  0.527913  0.666643  1.000000
```

---

## Teste 1: Baseline Multivariado Puro (O Ponto de Partida)
**Objetivo:** Estabelecer o marco zero de precisão preditiva utilizando apenas os dados brutos de fechamento das ações, servindo como referencial mínimo a ser superado.  
**Arquitetura:** LSTM Simples (Multivariada para 4 alvos).  
**Resultado Literal:**
```text
==================================================
 RESULTADO OFICIAL DO BASELINE PURO (100 REDES)
==================================================
MAPE MSFT: 2.03%
MAPE NVDA: 3.55%
MAPE GOOGL: 3.78%
MAPE META: 4.72%
--------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA: 3.52%
==================================================
```

---

## Teste 2: O Baseline "Megazord" (Engenharia de Atributos Simultânea)
**Objetivo:** Avaliar o impacto preditivo da inserção abrupta de 50 variáveis financeiras e macroeconômicas (OHLCV, Médias, MACD, RSI, Bandas de Bollinger, S&P 500 e VIX).  
**Arquitetura:** LSTM Simples (Capacidade paramétrica inalterada).  
**Resultado Literal:**
```text
==================================================
 RESULTADO OFICIAL DO BASELINE MEGAZORD (100 REDES)
==================================================
MAPE Microsoft: 3.37%
MAPE Nvidia: 5.75%
MAPE Alphabet: 5.09%
MAPE Meta: 7.11%
--------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA: 5.33%
==================================================
```

---

## Teste 3: Aumento de Capacidade Paramétrica (LSTM 128) + Hit Rate
**Objetivo:** Ajustar a rede à Maldição da Dimensionalidade criada pelas 50 variáveis, aumentando o número de neurônios para expandir o espaço cognitivo do modelo e introduzindo a métrica de acerto direcional.  
**Arquitetura:** LSTM Larga (128 Neurônios).  
**Resultado Literal:**
```text
==================================================
 RESULTADOS DO TESTE 3: LSTM 128 (100 REDES)
==================================================
Microsoft (MSFT):
  - MAPE: 2.84%
  - Hit Rate: 52.08%
Nvidia (NVDA):
  - MAPE: 4.04%
  - Hit Rate: 46.73%
Alphabet (GOOGL):
  - MAPE: 4.18%
  - Hit Rate: 55.36%
Meta Platforms (META):
  - MAPE: 5.39%
  - Hit Rate: 47.62%
--------------------------------------------------
MAPE GLOBAL: 4.11%
HIT RATE GLOBAL: 50.45%
==================================================
```

---

## Teste 4: Arquitetura Bi-LSTM e Avaliação Direcional (Hit Rate)
**Objetivo:** Avaliar se a leitura bidirecional do tempo (capturando o contexto cronológico do passado para o futuro e vice-versa) melhora a taxa de acerto do modelo frente a séries financeiras.  
**Arquitetura:** Bidirectional LSTM (Bi-LSTM).  
**Resultado Literal:**
```text
==================================================
 RESULTADOS DO TESTE 3: BI-LSTM (100 REDES)
==================================================
Microsoft (MSFT):
  - MAPE: 2.52%
  - Direção Correta (Hit Rate): 52.98%
Nvidia (NVDA):
  - MAPE: 3.32%
  - Direção Correta (Hit Rate): 47.92%
Alphabet (GOOGL):
  - MAPE: 3.10%
  - Direção Correta (Hit Rate): 56.25%
Meta Platforms (META):
  - MAPE: 4.02%
  - Direção Correta (Hit Rate): 48.51%
--------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA: 3.24%
HIT RATE MÉDIO DO PORTFÓLIO: 51.41%
==================================================
```

---

## Teste 5 (Revisado): Busca em Grade de Alta Resolução Temporal
**Objetivo:** Determinar empiricamente qual é a janela de memória (Lookback Window) ótima para processar o ecossistema de Inteligência Artificial sem causar saturação de memória.  
**Método:** Algoritmo Grid Search avaliando janelas de 10 a 60 dias.  
**Resultado Literal:**
```text
============================================================
 RANKING DEFINITIVO DOS TAMANHOS DE JANELA (seq_len)
============================================================
Janela: 20 dias --> MAPE: 3.14% | Hit Rate: 51.16%
Janela: 30 dias --> MAPE: 3.18% | Hit Rate: 50.95%
Janela: 60 dias --> MAPE: 3.18% | Hit Rate: 51.93%
Janela: 45 dias --> MAPE: 3.22% | Hit Rate: 51.33%
Janela: 25 dias --> MAPE: 3.23% | Hit Rate: 51.60%
Janela: 10 dias --> MAPE: 3.36% | Hit Rate: 52.17%
Janela: 15 dias --> MAPE: 3.37% | Hit Rate: 51.38%
============================================================
```

---

## Teste 6: Otimização Bayesiana de Hiperparâmetros (Optuna)
**Objetivo:** Encontrar matematicamente o equilíbrio perfeito entre a densidade de neurônios da Bi-LSTM e o tamanho dos passos da correção de erro (Learning Rate).  
**Método:** Busca Bayesiana via framework Optuna.  
**Resultado Literal:**
```text
============================================================
 PARÂMETROS MATEMÁTICOS ABSOLUTOS ENCONTRADOS
============================================================
Neurônios na Camada Oculta Bi-LSTM: 256
Taxa de Aprendizado (Learning Rate): 0.000813
============================================================
```

---

## Teste 7: Arquitetura de Estado da Arte (Bi-LSTM + Bi-GRU + Dropout)
**Objetivo:** Testar o impacto da profundidade empilhando dois blocos complexos de memória com regulação (Dropout) para evitar o over-fitting das 50 variáveis.  
**Arquitetura:** Camada 1 (Bi-LSTM) seguida de Camada 2 (Bi-GRU) com Dropout.  
**Resultado Literal:**
```text
==================================================
 RESULTADOS DO TESTE 7: ARQUITETURA SUPREMA
==================================================
Microsoft (MSFT):
  - MAPE: 3.48%
  - Direção Correta (Hit Rate): 52.91%
Nvidia (NVDA):
  - MAPE: 3.59%
  - Direção Correta (Hit Rate): 49.71%
Alphabet (GOOGL):
  - MAPE: 4.74%
  - Direção Correta (Hit Rate): 56.40%
Meta Platforms (META):
  - MAPE: 4.39%
  - Direção Correta (Hit Rate): 50.00%
--------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA: 4.05%
HIT RATE MÉDIO DO PORTFÓLIO: 52.25%
==================================================
```

---

## Teste 8: Arquitetura com Mecanismo de Atenção (Self-Attention)
**Objetivo:** Avaliar a eficiência da camada de Atenção em quebrar a linearidade da memória, focando pesos matemáticos em dias cruciais (sinal) e ignorando dias de lateralização (ruído).  
**Arquitetura:** Bi-LSTM (Única) acoplada à camada linear de Self-Attention.  
**Resultado Literal:**
```text
==================================================
 RESULTADOS DO TESTE 8: ATENÇÃO CRUZADA
==================================================
Microsoft (MSFT):
  - MAPE: 2.19%
  - Hit Rate: 53.49%
Nvidia (NVDA):
  - MAPE: 2.92%
  - Hit Rate: 49.13%
Alphabet (GOOGL):
  - MAPE: 3.25%
  - Hit Rate: 56.40%
Meta Platforms (META):
  - MAPE: 3.39%
  - Hit Rate: 49.13%
--------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA: 2.94%
HIT RATE MÉDIO DO PORTFÓLIO: 52.03%
==================================================
```

---

## Teste 9: Otimização Bayesiana da Arquitetura de Estado da Arte (Optuna)
**Objetivo:** Recalibrar a densidade paramétrica estritamente para o novo modelo acoplado à mecânica de Atenção.  
**Método:** Busca Bayesiana via framework Optuna.  
**Resultado Literal:**
```text
============================================================
 PARÂMETROS MATEMÁTICOS ABSOLUTOS (ARQUITETURA FINAL)
============================================================
Neurônios na Camada Oculta Bi-LSTM: 352
Taxa de Aprendizado (Learning Rate): 0.001130
============================================================
```

---

## Evolução Arquitetural: Rede Profunda (Stacked Bi-LSTM) + Atenção Cruzada
**Objetivo:** Verificar a viabilidade de escalar verticalmente a arquitetura campeã, submetendo o aprendizado a múltiplas rodadas de extração sequencial.  
**Arquitetura:** Bi-LSTM -> Bi-LSTM -> Self-Attention.  
**Resultado Literal:**
```text
============================================================
 RESULTADO - ARQUITETURA PROFUNDA (100 REDES)
============================================================
MAPE MSFT: 4.20%
MAPE NVDA: 8.58%
MAPE GOOGL: 7.32%
MAPE META: 10.91%
------------------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA: 7.75%
============================================================
```

---

## Teste 10: Otimização Bayesiana da Arquitetura Profunda (Funil Assimétrico)
**Objetivo:** Encontrar a compressão de dimensionalidade ótima para interligar duas camadas sequenciais densas sem causar perda de sinal ou dissipação de gradiente.  
**Método:** Busca Bayesiana de topologia em funil.  
**Resultado Literal:**
```text
============================================================
 PARÂMETROS MATEMÁTICOS ABSOLUTOS (REDE PROFUNDA)
============================================================
Neurônios Camada 1 (Leitura): 320
Neurônios Camada 2 (Compressão): 192
Taxa de Aprendizado (Learning Rate): 0.000143
============================================================
```

---

## Teste 11: Validação da Arquitetura Profunda (Funil) com Métricas de Risco
**Objetivo:** Testar empiricamente os parâmetros do Optuna e comprovar a hipótese da Maldição da Profundidade observando o impacto do erro em dólares (MAE) e anomalias (RMSE).  
**Arquitetura:** Bi-LSTM(320) -> Bi-LSTM(192) -> Self-Attention.  
**Resultado Literal:**
```text
======================================================================
 RESULTADO OFICIAL - REDE PROFUNDA ASSIMÉTRICA (100 REDES)
======================================================================
Microsoft (MSFT):
  - MAPE: 4.06%
  - MAE: US$ 18.12 (Distância Média)
  - RMSE: US$ 21.73 (Volatilidade de Erro)
  - Hit Rate: 51.16%
Nvidia (NVDA):
  - MAPE: 5.09%
  - MAE: US$ 7.28 (Distância Média)
  - RMSE: US$ 8.71 (Volatilidade de Erro)
  - Hit Rate: 52.33%
Alphabet (GOOGL):
  - MAPE: 5.66%
  - MAE: US$ 13.55 (Distância Média)
  - RMSE: US$ 21.86 (Volatilidade de Erro)
  - Hit Rate: 52.62%
Meta Platforms (META):
  - MAPE: 7.46%
  - MAE: US$ 50.59 (Distância Média)
  - RMSE: US$ 61.61 (Volatilidade de Erro)
  - Hit Rate: 49.42%
----------------------------------------------------------------------
MAPE GLOBAL: 5.57%
MAE GLOBAL MÉDIO: US$ 22.39
HIT RATE GLOBAL: 51.38%
======================================================================
```

---

## Teste 12: A Arquitetura Profunda Definitiva (Res-LSTM + Layer Normalization)
**Objetivo:** Mitigar a degradação paramétrica e explosão de gradientes de redes profundas utilizando normalização de blocos e conexões residuais (atalhos matemáticos).  
**Arquitetura:** Bi-LSTM(320) -> Skip Connection + LayerNorm -> Bi-LSTM(192) -> Attention.  
**Resultado Literal:**
```text
======================================================================
 RESULTADO OFICIAL - REDE RES-LSTM PROFUNDA (100 REDES)
======================================================================
Microsoft (MSFT):
  - MAPE: 5.82%
  - MAE: US$ 26.62 (Distância Média)
  - RMSE: US$ 32.13 (Volatilidade de Erro)
  - Hit Rate: 50.00%
Nvidia (NVDA):
  - MAPE: 9.15%
  - MAE: US$ 14.10 (Distância Média)
  - RMSE: US$ 16.66 (Volatilidade de Erro)
  - Hit Rate: 49.71%
Alphabet (GOOGL):
  - MAPE: 8.24%
  - MAE: US$ 19.51 (Distância Média)
  - RMSE: US$ 30.54 (Volatilidade de Erro)
  - Hit Rate: 53.49%
Meta Platforms (META):
  - MAPE: 8.73%
  - MAE: US$ 58.36 (Distância Média)
  - RMSE: US$ 70.84 (Volatilidade de Erro)
  - Hit Rate: 49.71%
----------------------------------------------------------------------
MAPE GLOBAL: 7.98%
MAE GLOBAL MÉDIO: US$ 29.65
HIT RATE GLOBAL: 50.73%
======================================================================
```

---

## Teste de Trajetória (Multi-Step Forecast): Previsão Semanal (5 Dias)
**Objetivo:** Obrigar a rede neural de passo único a estender seu horizonte preditivo visando testar a abstração real da tendência contra a previsão ingênua (*Naive Forecast*).  
**Arquitetura:** Arquitetura Campeã Bi-LSTM (352) + Attention prevendo 20 targets simultâneos.  
**Resultado Literal:**
```text
======================================================================
 RESULTADO - PREVISÃO DE TRAJETÓRIA (5 DIAS NO FUTURO)
======================================================================
Microsoft (MSFT):
  - MAPE no Dia 1: 3.08%
  - MAPE no Dia 5: 4.26%
Nvidia (NVDA):
  - MAPE no Dia 1: 7.97%
  - MAPE no Dia 5: 9.77%
Alphabet (GOOGL):
  - MAPE no Dia 1: 6.14%
  - MAPE no Dia 5: 7.79%
Meta Platforms (META):
  - MAPE no Dia 1: 7.78%
  - MAPE no Dia 5: 9.56%
----------------------------------------------------------------------
MAPE GLOBAL DO ECOSSISTEMA (Dia 1): 6.24%
MAPE GLOBAL DO ECOSSISTEMA (Dia 5): 7.85%
======================================================================
```

---

## Teste 13: Otimização Direcional via Função de Perda Híbrida Customizada
**Objetivo:** Alterar a base matemática de punição da rede, penalizando-a severamente caso ela acerte a proximidade em dólares, mas erre a direção (sinal) real do movimento.  
**Método:** Substituição da MSELoss padrão por Função de Perda Híbrida Direcional (Multiplicador de 3x no erro de sinal).  
**Resultado Literal:**
```text
======================================================================
 RESULTADO OFICIAL - ARQUITETURA CAMPEÃ COM LOSS HÍBRIDA
======================================================================
Microsoft (MSFT):
  - MAPE: 2.49%
  - MAE: US$ 10.66 (Distância Média)
  - RMSE: US$ 12.85 (Volatilidade de Erro)
  - Hit Rate: 52.91%
Nvidia (NVDA):
  - MAPE: 2.93%
  - MAE: US$ 4.10 (Distância Média)
  - RMSE: US$ 5.27 (Volatilidade de Erro)
  - Hit Rate: 52.33%
Alphabet (GOOGL):
  - MAPE: 3.50%
  - MAE: US$ 7.91 (Distância Média)
  - RMSE: US$ 12.13 (Volatilidade de Erro)
  - Hit Rate: 56.10%
Meta Platforms (META):
  - MAPE: 3.35%
  - MAE: US$ 22.38 (Distância Média)
  - RMSE: US$ 27.70 (Volatilidade de Erro)
  - Hit Rate: 48.84%
----------------------------------------------------------------------
MAPE GLOBAL: 3.07%
MAE GLOBAL MÉDIO: US$ 11.26
HIT RATE GLOBAL: 52.54%
======================================================================
```

---

## Teste 14: Simulação de Mercado Real (Walk-Forward Validation com Fine-Tuning)
**Objetivo:** Simular um ambiente quantitativo real, anulando a deriva de conceito do mercado (Concept Drift) mediante o contínuo re-treinamento da arquitetura vencedora em pequenos recortes mensais.  
**Método:** Validação em Janela Expansiva com *Fine-Tuning* a cada bloco de 20 pregões.  
**Resultado Literal:**
```text
======================================================================
 RESULTADO OFICIAL - VALIDAÇÃO WALK-FORWARD (RE-TREINO MENSAL)
======================================================================
Microsoft (MSFT):
  - MAPE: 1.63%
  - MAE: US$ 7.22 (Erro Médio)
  - RMSE: US$ 9.27 (Volatilidade do Erro)
  - Hit Rate: 48.84%
Nvidia (NVDA):
  - MAPE: 2.85%
  - MAE: US$ 3.97 (Erro Médio)
  - RMSE: US$ 5.21 (Volatilidade do Erro)
  - Hit Rate: 52.62%
Alphabet (GOOGL):
  - MAPE: 2.04%
  - MAE: US$ 4.06 (Erro Médio)
  - RMSE: US$ 5.51 (Volatilidade do Erro)
  - Hit Rate: 55.23%
Meta Platforms (META):
  - MAPE: 1.93%
  - MAE: US$ 12.20 (Erro Médio)
  - RMSE: US$ 16.72 (Volatilidade do Erro)
  - Hit Rate: 47.67%
----------------------------------------------------------------------
MAPE GLOBAL: 2.11%
MAE GLOBAL MÉDIO: US$ 6.86
HIT RATE GLOBAL: 51.09%
======================================================================
```

---

## Teste Bônus: Simulador de Negociação (Backtesting Financeiro)
**Objetivo:** Avaliar a real rentabilidade gerada pelo algoritmo de precisão operando capital em ambiente virtual simulado versus a inércia passiva do mercado em forte ciclo de alta.  
**Método:** Simulação com capital alocado de US$ 10.000,00 confrontando estratégia de Buy & Hold com Estratégia Ativa Dinâmica Long-Only.  
**Resultado Literal:**
```text
============================================================
 RELATÓRIO DE PERFORMANCE FINANCEIRA (BACKTEST)
============================================================
Capital Inicial: US$ 10,000.00
------------------------------------------------------------
Estratégia Buy & Hold (Mercado Passivo):
  - Saldo Final: US$ 14,637.32
  - Retorno Acumulado: 46.37%
------------------------------------------------------------
Estratégia Gerida pela IA (Walk-Forward):
  - Saldo Final: US$ 12,968.21
  - Retorno Acumulado: 29.68%
============================================================
```
