# Air Passengers Time Series Analysis

Este projeto consiste em uma análise detalhada e modelagem preditiva de séries temporais utilizando o clássico dataset "Air Passengers" (Passageiros de Companhias Aéreas). O objetivo principal é analisar o comportamento histórico do volume de passageiros, entender as características da série (tendência e sazonalidade) e construir um modelo capaz de prever com precisão o volume de passageiros para os 12 meses seguintes (ano de 1961).

## 🎯 Objetivos

- Realizar Análise Exploratória de Dados (EDA) em séries temporais.
- Verificar a normalidade e a estacionaridade dos dados usando testes estatísticos (Shapiro-Wilk, KPSS, Dickey-Fuller Adicional).
- Aplicar transformações (logarítmica e diferenciações) para converter a série em estacionária.
- Avaliar gráficos de Autocorrelação (ACF) e Autocorrelação Parcial (PACF).
- Testar e comparar modelos de previsão da família ARIMA e SARIMA.
- Validar os resíduos dos modelos desenvolvidos (ruído branco).
- Gerar previsões futuras e exportar os resultados.

## 🛠️ Tecnologias e Bibliotecas Utilizadas

O projeto foi desenvolvido em Python, utilizando as seguintes bibliotecas principais:

- **Manipulação e Análise de Dados:** `pandas`, `numpy`
- **Visualização:** `matplotlib`, `seaborn`
- **Modelagem e Estatística:** `statsmodels`, `scipy`, `scikit-learn`, `pmdarima`
- **Obtenção de Dados:** `kagglehub`

## 📊 Base de Dados

O dataset utilizado é obtido diretamente do Kaggle através da biblioteca `kagglehub` (`rakannimer/air-passengers`).
Ele contém o registro mensal do total de passageiros de companhias aéreas internacionais, entre 1949 e 1960.

## 🧠 Metodologia Aplicada

1. **Análise Inicial e Testes Estatísticos:**
   - Visualização da série indicando uma forte tendência de alta e sazonalidade clara.
   - Aplicação dos testes QQ-Plot e Shapiro-Wilk para verificar normalidade.
   - Aplicação dos testes KPSS e Augmented Dickey-Fuller (ADF) para verificar estacionaridade.

2. **Transformações da Série:**
   - **Transformação Logarítmica:** Aplicada para estabilizar a variância (que aumentava com o tempo).
   - **Diferenciação:** Aplicada para remover a tendência e sazonalidade, tornando a série estacionária. Foram necessárias duas diferenciações na análise de modelo ARMA.

3. **Modelagem:**
   - Inicialmente, foi avaliado um modelo **ARIMA (1,0,1)** nos dados duplamente diferenciados. A análise dos resíduos (Ljung-Box, Shapiro-Wilk) indicou que ainda existia informação sazonal não capturada.
   - Posteriormente, o foco passou para modelos **SARIMAX**, avaliando diferentes ordens de integração de forma automatizada (funções `ndiffs` e `nsdiffs`).
   - Foram ajustados e comparados três modelos SARIMA:
     - SARIMAX(1,d,0)(0,D,0,12)
     - SARIMAX(1,d,1)(0,D,0,12)
     - **SARIMAX(0,1,1)(0,1,1)_12 (Melhor Modelo)**

4. **Validação do Modelo:**
   - O melhor modelo foi definido avaliando os resíduos, garantindo que se comportassem como Ruído Branco (independentes e sem autocorrelação significativa).

## 📈 Resultados do Melhor Modelo

O modelo selecionado para previsões finais foi o **SARIMAX(0,1,1)(0,1,1)_12**. O desempenho do modelo com os dados de teste gerou as seguintes métricas:

- **MAE (Erro Médio Absoluto):** Mede o erro absoluto médio das previsões.
- **RMSE (Raiz do Erro Quadrático Médio):** Penaliza erros maiores, oferecendo uma boa visão geral da precisão do modelo.
- **MAPE (Erro Percentual Absoluto Médio):** Mede o erro em porcentagem.

As previsões para o ano de 1961 (próximos 12 meses não observados) foram geradas com um intervalo de confiança de 95% e plotadas graficamente para visualização intuitiva.

No final da execução, as previsões mensais são exportadas e salvas no arquivo Excel `Previões de passageiros para 1961.xlsx`.

## 🚀 Como Executar

1. Certifique-se de ter o Python instalado.
2. É recomendável o uso de um ambiente virtual (venv ou conda).
3. Instale as dependências necessárias executando:
   ```bash
   pip install numpy pandas matplotlib seaborn statsmodels scipy scikit-learn pmdarima openpyxl kagglehub
   ```
4. Execute o script principal:
   ```bash
   python estudo_air_passangers.py
   ```
5. O script irá baixar os dados via API do Kaggle, imprimir os resumos de testes e plotar os gráficos das análises. Ao final, o arquivo `.xlsx` com as projeções será criado no diretório raiz.
