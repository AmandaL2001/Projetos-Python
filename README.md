# Projetos-Python
Este repositório tem como objetivo apresentar os meus projetos feitos em python, para comparar a minha evolução conforme vou praticando

# Índice

# Painel COVID e COVID-19 - Projeto EBAC : Dados referente aos casos de contaminação, mortes e vacinação pelo Brasil apresentados pelo Loocker Studio, juntamente com a documentação referente a extração, limpeza e manipulação dos dados:

A COVID-19 é a doença causada por um novo coronavírus denominado SARS-CoV-2. A Organização Mundial da Saúde (OMS) tomou conhecimento deste novo vírus em 31 de dezembro de 2019, após receber a notificação de um grupo de casos de “pneumonia viral” em Wuhan, na República Popular da China.

Os dados apresentados mostram o impacto que o virus causou na vida de milhares de pessoas, em especial, o Estado de São Paulo, o mais populoso do Brasil.

Os dados abaixo não se tratam de apenas números, mas sim de pessoas que tinham uma vida, sonhos, ambições, mas que infelizmente foram interrompidos pelo vírus.

A autora deste notebook presta solidariedade a todas as pessoas e seus familiares que tiveram suas vidas ceifadas

-Pacotes e bibliotecas: 

import math
from typing import Iterator
from datetime import datetime, timedelta

import numpy as np
import pandas as pd

-Fonte de dados: cases = pd.read_csv('https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_daily_reports/01-12-2021.csv', sep=',')

![image](https://github.com/user-attachments/assets/fc1fb1ec-ae49-48c7-b606-39599e8de9d9)


# Integração AWS IAM / S3 / Athena: Tem por objetivo realizar o particionamento do arquivo extraido em aula, diminuindo os custos e a velocidade de processamento, além de facilitar na manipulação dos dados e criação de dashboards.

Foi feito a integração entre o Github e o AWS. 

-Pacotes e Bibliotecas: 

import pandas as pd
from datetime import datetime
from getpass import getpass
import boto3

-Fonte de dados: !wget https://raw.githubusercontent.com/andre-marcos-perez/ebac-course-utils/main/dataset/crime.csv -q -O crime.csv

# Loggi - Projeto EBAC -  O OBJETIVO É ENTENDER MELHOR O(S) PROBLEMA(S) E ATRAVES DOS DADOS DESENVOLVER SOLUÇÕES EFICAZES PARA A OTIMIZAÇÃO DAS ROTAS DE ENTREGA, ALOCAÇÃO DE ENTREGAS NOS VEÍCULOS DA FROTA COM CAPACIDADE LIMITADA ETC.

-Pacotes e Bibliotecas: 

import json
import pandas as pd
import seaborn as sns

- Fonte de dados: !wget -q "https://raw.githubusercontent.com/andre-marcos-perez/ebac-course-utils/main/dataset/deliveries.json" -O deliveries.json

![image](https://github.com/user-attachments/assets/a743dd20-2adf-4c27-8e23-1ed492b5af7d)


# Projeto API - Telegram/AWS: 

![image](https://github.com/user-attachments/assets/c70520fe-3b4b-410a-8a2d-c9152b67b4a1)

Telegram
O Telegram representa a fonte de dados transacionais. Mensagens enviadas por usuários em um grupo são capturadas por um bot e redirecionadas via webhook do backend do aplicativo para um endpoint (endereço web que aceita requisições HTTP) exposto pelo AWS API Gateway. As mensagens trafegam no corpo ou payload da requisição.

AWS | Ingestão
Uma requisição HTTP com o conteúdo da mensagem em seu payload é recebia pelo AWS API Gateway que, por sua vez, as redireciona para o AWS Lambda, servindo assim como seu gatilho. Já o AWS Lambda recebe o payload da requisição em seu parâmetro event, salva o conteúdo em um arquivo no formato JSON (original, mesmo que o payload) e o armazena no AWS S3 particionado por dia.

AWS | ETL
Uma vez ao dia, o AWS Event Bridge aciona o AWS Lambda que processa todas as mensagens do dia anterior (atraso de um dia ou D-1), denormaliza o dado semi-estruturado típico de arquivos no formato JSON, salva o conteúdo processado em um arquivo no formato Apache Parquet e o armazena no AWS S3 particionado por dia.

AWS | Apresentação
Por fim, uma tabela do AWS Athena é apontada para o bucket do AWS S3 que armazena o dado processado: denormalizado, particionado e orientado a coluna. Profissionais de dados podem então executar consultas analíticas (agregações, ordenações, etc.) na tabela utilizando o SQL para a extração de insights.

-Pacotes e Bibliotecas:

import os
import json
import logging
from datetime import datetime, timedelta, timezone
import boto3
import pyarrow as pa
import pyarrow.parquet as pq


     
