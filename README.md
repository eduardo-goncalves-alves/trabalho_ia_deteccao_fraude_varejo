# Detecção de Fraudes em Transações de Varejo


Este repositório contém o desenvolvimento de um pipeline completo de Machine Learning para identificar transações financeiras fraudulentas, focado em dados de e-commerce e varejo. O projeto engloba desde a Análise Exploratória de Dados (EDA) até o treinamento e avaliação de modelos supervisionados e não supervisionados.


## Dataset


**Retail Intelligence Fraud Detection Dataset** O arquivo principal utilizado é o `retail_fraud_detection_100k.csv`. Ele contém 100.000 registros com atributos relacionados a pagamentos, contexto do dispositivo, localização e indicadores comportamentais.


> **Nota Técnica:** Durante o pré-processamento, variáveis preditivas determinísticas (flags pré-calculadas) foram removidas para evitar *Data Leakage* (vazamento de dados) e simular um ambiente de produção realista onde o modelo precisa aprender com os dados brutos da transação.


## Tecnologias Utilizadas


* **Python 3**
* **Google Colab:** Ambiente de execução em nuvem
* **Pandas & Numpy:** Manipulação e tratamento de dados
* **Matplotlib & Seaborn:** Visualização de dados
* **Scikit-Learn:** Pré-processamento, Regressão Logística, Random Forest e Isolation Forest
* **XGBoost:** Classificador de Gradiente Extremo


## Como Executar o Projeto (Google Colab)


Para testar o pipeline sem precisar instalar dependências na sua máquina, siga os passos abaixo:


1. Baixe o dataset `retail_fraud_detection_100k.csv` e o arquivo do notebook (`.ipynb`) deste repositório para o seu computador.
2. Acesse o [Google Colab](https://colab.research.google.com/).
3. No menu inicial do Colab, vá na aba **Upload** (Fazer upload) e envie o arquivo `.ipynb` do projeto.
4. Com o notebook aberto, clique no ícone de **Pasta** (Arquivos) no menu lateral esquerdo.
5. Clique no ícone de upload (uma folha com uma seta para cima) e envie o dataset `retail_fraud_detection_100k.csv` para a sessão.
6. No menu superior, clique em **Ambiente de execução** e depois em **Executar tudo**. O notebook rodará sequencialmente do carregamento dos dados até a avaliação final dos modelos.


## Resultados e Conclusões


Foram treinados e comparados três modelos supervisionados e um modelo de detecção de anomalias, todos lidando com o desbalanceamento natural de classes.


| Modelo | ROC-AUC | Observações |
| :--- | :--- | :--- |
| **Regressão Logística** | 0.8717 | Ótimo baseline, mas com limitações para capturar não-linearidades. |
| **Random Forest** | 0.9039 | Bom avanço e equilíbrio geral entre precisão e recall. |
| **XGBoost** | **0.9061** | **Modelo vencedor.** Maior poder de distinção entre classes. |


**Veredito:** O **XGBoost** foi o modelo mais adequado. Além de apresentar a maior métrica ROC-AUC, ele obteve o maior *Recall* para fraudes (83%). No ecossistema do varejo digital, essa métrica é crucial para identificar e barrar fraudes reais, minimizando as pesadas perdas financeiras geradas por *chargebacks*, o que torna esse algoritmo o mais indicado para uma integração em produção.


O modelo não supervisionado (Isolation Forest) serviu como validação de anomalias generalistas, mas mostrou-se menos eficiente na classificação direta devido ao alto volume de falsos positivos.






