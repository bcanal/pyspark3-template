# Pyspark3 template

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

### Resumo
O projeto cria uma estrutura baseada no Poetry usando o requests como dependencia e empacotanto a aplicação com o build do poetry e as dependencias com o pex

### Requerimentos
 - python ^3.9
 - Poetry ^1.1 (guide Poetry install: https://python-poetry.org/docs/)
 - Apache Spark >= 3.1 (guide apache spark install: https://spark.apache.org/downloads.html)

### Criação do Projeto
 1. Criar estrutura com Poetry e adicionar a dependencia requests
    ```
    poetry new pyspark3-template
    cd pyspark3-template && poetry add requests
    ```
 2. Adicionar no virtualenv o pex
    ```
    poetry shell
    pip install "pex>=2.1"
    ```
 3. Criar um arquivo app.py no path do projeto, com o código
    ```
    import requests
    r = requests.get('https://api.github.com')
    print(r.status_code)
    ```
 4. Build da Aplicação
    ```
    poetry build
    ```
 5. Empacotamento das dependências
    ```
    poetry export -f requirements.txt --output requirements.txt
    pex -r requirements.txt -o dependencies.pex
    deactivate
    ```
 6. Spark Submit Code:
    ```
    cd pyspark3-template && \
    spark-submit \
      --master local \
      --conf spark.pyspark.python=./dependencies.pex \
      --py-files ./dist/pyspark3_template-0.1.0-py3-none-any.whl \
      app.py
    ```
