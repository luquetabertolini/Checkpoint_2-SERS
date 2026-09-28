# Análise de Dados de Energia Renovável com APIs e Machine Learning

## Objetivo

Este projeto tem como objetivo utilizar dados de geração de energia e condições meteorológicas para realizar análises e aplicar algoritmos de Machine Learning.

O notebook realiza o tratamento e a análise dos dados, além da aplicação de modelos de **classificação e regressão**, permitindo comparar diferentes algoritmos e avaliar seu desempenho.

Na etapa de regressão, o objetivo é estimar a **radiação solar horizontal média (`radiacao_w_m2`)** a partir de cinco variáveis de entrada:

* `temperatura_c`
* `umidade_pct`
* `nuvens_pct`
* `vento_kmh`
* `hora`

A variável `radiacao_w_m2` é utilizada exclusivamente como variável alvo, não sendo utilizada como entrada do mesmo registro.

---

## Fontes dos dados

Os dados utilizados no projeto são provenientes das seguintes fontes:

* **ANEEL — SIGA (Sistema de Informações de Geração da ANEEL):**
  https://dadosabertos.aneel.gov.br/dataset/siga-sistema-de-informacoes-de-geracao-da-aneel

* **ANEEL — Recurso e campos utilizados:**
  https://dadosabertos.aneel.gov.br/dataset/siga-sistema-de-informacoes-de-geracao-da-aneel/resource/11ec447d-698d-4ab8-977f-b424d5deee6a

* **Open-Meteo — Historical Weather API:**
  https://open-meteo.com/en/docs/historical-weather-api

Os dados meteorológicos utilizados na etapa de regressão contêm registros de condições atmosféricas e radiação solar, organizados cronologicamente pela variável `data_hora`.

### Variáveis meteorológicas

| Variável        | Descrição                               |
| --------------- | --------------------------------------- |
| `data_hora`     | Data e hora local do registro           |
| `temperatura_c` | Temperatura do ar em °C                 |
| `umidade_pct`   | Umidade relativa do ar em %             |
| `nuvens_pct`    | Cobertura de nuvens em %                |
| `vento_kmh`     | Velocidade do vento em km/h             |
| `hora`          | Hora local do registro                  |
| `radiacao_w_m2` | Radiação solar horizontal média em W/m² |

---

## Estrutura do projeto

O repositório deve conter:

```text
├── README.md
├── Aula_APIs_Energia_Renovavel_ML.ipynb
├── *.csv
└── figuras/
```

Os arquivos CSV utilizados no notebook devem estar disponíveis no repositório ou possuir instruções completas para sua reprodução.

---

## Como executar

### 1. Clonar o repositório

```bash
git clone URL_DO_REPOSITORIO
cd NOME_DO_REPOSITORIO
```

### 2. Instalar as dependências

O notebook utiliza Python e bibliotecas para manipulação de dados, visualização e Machine Learning.

As principais bibliotecas utilizadas são:

```bash
pip install pandas matplotlib seaborn scikit-learn
```

Caso as etapas anteriores do notebook utilizem bibliotecas adicionais para acesso às APIs, elas também devem ser instaladas no ambiente.

### 3. Abrir o notebook

O arquivo `.ipynb` pode ser executado utilizando Jupyter Notebook, JupyterLab ou Google Colab.

```bash
jupyter notebook
```

Depois, abra o arquivo:

```text
Aula_APIs_Energia_Renovavel_ML.ipynb
```

### 4. Executar as células

As células devem ser executadas **na ordem**, começando por um ambiente limpo.

Os arquivos CSV necessários devem estar no local esperado pelo notebook. Na etapa de regressão, por exemplo, o arquivo utilizado é:

```text
meteo_regressao_orange.csv
```

---

## Metodologia — Regressão

A etapa de regressão mantém os registros em ordem cronológica pela coluna `data_hora`.

Os dados são divididos aproximadamente em:

* **80% das primeiras horas:** treinamento;
* **20% das horas finais:** teste.

Não é realizado embaralhamento dos registros, preservando a ordem temporal.

Foram utilizados três algoritmos:

1. **Regressão Linear**

   * Utilizada como modelo de referência.
   * É um modelo simples que permite avaliar uma relação linear entre as variáveis.

2. **Random Forest Regressor**

   * Modelo baseado em várias árvores de decisão.
   * É capaz de representar relações não lineares entre as variáveis.

3. **Gradient Boosting Regressor**

   * Utiliza árvores construídas sequencialmente para corrigir erros dos modelos anteriores.
   * Permite representar relações mais complexas nos dados.

---

## Métricas utilizadas

Os modelos de regressão são comparados utilizando:

* **MAE (Mean Absolute Error):** erro absoluto médio em W/m².
* **MSE (Mean Squared Error):** erro quadrático médio em (W/m²)².
* **R² (coeficiente de determinação):** indica a proporção da variabilidade da variável alvo explicada pelo modelo.

### Resultados da regressão

| Modelo            | MAE (W/m²) | MSE ((W/m²)²) |     R² |
| ----------------- | ---------: | ------------: | -----: |
| Regressão Linear  |     145.20 |      30034.20 | 0.3598 |
| Random Forest     |      66.40 |       7210.08 | 0.8463 |
| Gradient Boosting |      67.77 |       7419.76 | 0.8419 |

Os resultados mostram diferenças importantes entre os três modelos. A Regressão Linear apresentou MAE e MSE maiores e R² menor, enquanto os modelos baseados em árvores apresentaram valores de erro menores e maior R² no conjunto de teste.

Também foi gerado um gráfico comparando os valores reais e previstos de radiação solar para o modelo Random Forest.

---

## Importância das variáveis

A análise de impo
