## PRÁTICA COM O FRAMEWORK SPARK 🐸

O objetivo desse repositório é demonstrar uma prática com o framework Spark, uma ferramenta fantástica para processamento distribuído. Essa prática foi desenvolvida no docker!

---

📢 ETAPA 1: ENVIANDO O ARQUIVO PARA O HDFS

> Enviar o diretório local “/input/exercises-data/juros_selic” para o HDFS em “/user/aluno/gabriel/data”

O nosso objetivo é enviar todos os arquivos do diretório “/input/exercises-data/juros_selic” para o HDFS. Para isso, vamos aplicar o seguinte comando

``` bash
$ hdfs dfs  -put /input/exercises-data/juros_selic/ /user/aluno/gabriel/data
``` 

![Etapa 1](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_1.png?raw=true)

📢 ETAPA 2: CRIANDO O DATAFRAME

> Criar o DataFrame jurosDF para ler o arquivo no HDFS “/user/aluno/<nome>/data/juros_selic/juros_selic.json”

Utilizando o Spark, vamos criar um DF para ler o arquio "juros_selic.json". Vale lembrar que o Spark não modifica o arquivo primário, então precisamos criar uma val nova e carregar os arquivos, e para isso, vamos utilizar o seguinte comando:
``` bash
$ val jurosDF = spark.read.json("/user/aluno/gabriel/data/juros_selic.json")
``` 

![Etapa 2](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_2.png?raw=true)

📢 ETAPA 3: VISUALIZANDO SCHEMA

> Visualizar o Schema do jurosDF

Para visualizar o schema da val jurosDF, vamos aplicar a seguinte consulta:
``` bash
$ jurosDF.printSchema
``` 
![Etapa 3](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_3.png?raw=true)

📢 ETAPA 4: EXIBINDO OS REGISTROS

> Mostrar os 10 primeiros registros do jutosDF

Agora no passo 4, queremos exibir os 10 primeiros registros do jurosDF, para isso vamos utilizar o comando:
``` bash
$ jurosDF.show(10, false)
``` 

![Etapa 5](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_4.png?raw=true)

📢 ETAPA 5: NÚMEROS DE REGISTROS

> Contar a quantidade de registros do jurosDF

Agora uma etapa bem simples, vamos contar o número de registros com o comando:
``` bash
$ jurosDF.count
``` 
![Etapa 5](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_5.png?raw=true)


