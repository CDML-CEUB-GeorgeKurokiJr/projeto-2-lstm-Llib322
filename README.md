Previsão de Ações da Microsoft (MSFT): Uma Abordagem com Bi-LSTMs e Otimização Bayesiana

Este repositório contém o projeto de conclusão focado na previsão de séries temporais financeiras (ações da Microsoft) utilizando Deep Learning. O objetivo deste trabalho não foi apenas criar um modelo preditivo, mas realizar um Estudo de Ablação exaustivo para provar matematicamente quais arquiteturas, variáveis e janelas de tempo funcionam melhor no mercado financeiro.

O modelo final atingiu um MAPE (Erro Percentual Absoluto Médio) de 1.27%, operando no limite do ruído estatístico (Noise Floor) da bolsa de valores.

Guia do Repositório (Por onde começar?)
Para facilitar a avaliação, o repositório está organizado da seguinte forma:

LSTM_projeto_2_versao_final.ipynb: ESTE É O ARQUIVO PRINCIPAL. É o notebook que deve ser avaliado. Ele contém o código final limpo, organizado, comentado em blocos estruturados e com as explicações detalhadas em Markdown sobre o nosso modelo definitivo.

Sabe mt ou sabe pouco.ipynb: Este notebook contém a execução bruta e a prova real do teste final. É no final deste documento que o código rodou o Ensemble massivo de 2.000 redes neurais para cravar o resultado oficial de 1.27%.

notebooks/: Esta pasta contém o "chão de fábrica" do projeto. Aqui estão quase todos os códigos de testes, rascunhos e falhas iterativas. Estão desorganizados propositalmente, pois representam o processo real de tentativa e erro da pesquisa. Caso queira ver a evolução crua do código, os arquivos estão à disposição.

documents/: Pasta contendo os artefatos visuais e de dados. Inclui gráficos gerados, logs de resultados de testes realizados ao longo do tempo e as duas tabelas .csv finais contendo os valores das previsões vs. preços reais (para o teste cego e previsões futuras).

A Jornada Metodológica (Passo a Passo)
Para chegar à arquitetura final, não adotamos o senso comum de tentar a rede neural mais complexa possível. Testamos hipótese por hipótese:

O "Megazord" de Dados (Feature Engineering): Abandonamos a previsão baseada apenas no preço de fechamento. Construímos uma matriz com 17 colunas que alimentam a IA com o contexto completo: indicadores técnicos (RSI, MACD, Bandas de Bollinger, Médias Móveis) e termômetros macroeconômicos (Índice S&P 500 e Índice de Volatilidade VIX).

Estudo de Ablação (Simplicidade > Complexidade): * Mecanismo de Atenção: Testado e rejeitado. Gerou um efeito indesejado de média móvel (over-smoothing).

Dropout (Esquecimento): Testado e rejeitado. No mercado financeiro, a relação sinal/ruído é baixa, e forçar a rede a "esquecer" gerou underfitting.

Campeã: Uma Bi-LSTM Pura, capaz de ler os dados temporalmente de forma bidirecional.

A Descoberta do Tempo (Janela de 30 Dias): Rodamos uma Busca em Grade (Grid Search) testando memórias de 10 a 60 dias. A matemática provou que a MSFT tem "memória curta": 30 dias úteis (1 mês e meio) foi o ponto de equilíbrio perfeito entre filtrar ruídos e não utilizar dados velhos.

Busca Exaustiva de Hiperparâmetros (Optuna): Deixamos a inteligência artificial (Optuna) rodar 500 tentativas para mapear o relevo matemático perfeito, encontrando a configuração ideal de 128 neurônios na LSTM, 144 na GRU e uma taxa de aprendizado de 0.000874.

A Prova Final (Ensemble de 2.000 Modelos): Para eliminar qualquer viés de inicialização de pesos (sorte estatística), a arquitetura final não é uma rede, mas a média absoluta de 2.000 redes neurais independentes.

Tecnologias Utilizadas
Linguagem: Python

Deep Learning: PyTorch

Otimização: Optuna (Otimização Bayesiana)

Manipulação de Dados e Finanças: Pandas, Scikit-Learn, NumPy e yfinance.
