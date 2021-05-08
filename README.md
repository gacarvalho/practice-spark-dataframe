## PRÁTICA COM O FRAMEWORK SPARK 🟠

O objetivo desse repositório é demonstrar uma prática com o framework Spark com scala, uma ferramenta fantástica para processamento distribuído. Essa prática foi desenvolvida no docker!

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
scala> val jurosDF = spark.read.json("/user/aluno/gabriel/data/juros_selic.json")
``` 

![Etapa 2](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_2.png?raw=true)

📢 ETAPA 3: VISUALIZANDO SCHEMA

> Visualizar o Schema do jurosDF

Para visualizar o schema da val jurosDF, vamos aplicar a seguinte consulta:
``` bash
scala> jurosDF.printSchema
``` 
![Etapa 3](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_3.png?raw=true)

📢 ETAPA 4: EXIBINDO OS REGISTROS

> Mostrar os 10 primeiros registros do jutosDF

Agora no passo 4, queremos exibir os 10 primeiros registros do jurosDF, para isso vamos utilizar o comando:
``` bash
scala> jurosDF.show(10, false)
``` 

![Etapa 5](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_4.png?raw=true)

📢 ETAPA 5: NÚMEROS DE REGISTROS

> Contar a quantidade de registros do jurosDF

Agora uma etapa bem simples, vamos contar o número de registros com o comando:

``` bash
scala> jurosDF.count
``` 
![Etapa 5](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_5.png?raw=true)


📢 ETAPA 6: CRIANDO O DATAFRAME jurosDF10

> Criar o DataFrame jurosDF10 para filtrar apenas os registros com o campo “valor” maior que 10

Para o desenvolvimento da etapa 6, vamos criar um novo DF chamado de jurosDF10 filtrando registros apenas maiores do que 10. Para isso, vamos utilizar o comando: 
``` bash
scala> val jurosDF10 = jurosDF.where("valor > 10")
``` 
![Etapa 6](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_6.png?raw=true)


📢 ETAPA 7: SALVANDO O DF como tabela interna no Hive

> Salvar o DataFrame jurosDF10  como tabela Hive “empresastartup.tab_juros_selic”

Para salvarmos o dataframe como tabela interna no hive, utilizamos o comando 
``` bash
scala> val jurosDF10.write.saveAsTable("empresastartup.tab_juros_selic")
``` 
![Etapa 7](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_7.png?raw=true)


📢 ETAPA 8: LENDO A TABELA CRIADA NO HIVE

> Criar o DataFrame jurosHiveDF para ler a tabela “empresastartup.tab_juros_selic”
> Visualizar o Schema do jurosHiveDF
> Mostrar os 5 primeiros registros do jurosHiveDF

O primeiro passo para realizar e etapa 8, vamos criar um novo dataframe para ler a tabela que foi salva no Hive com o nome "tab_juros_selic", e para isso, precisamos ler a tabela com o comando:
``` bash
scala> val jurosHiveDF = spark.read.table("empresastartup.tab_juros_selic")
``` 
Depois de carregar a tabela "tab_juros_selic" na val "jurosHiveDF", vamos observar o schema e analisar os primeiros 5 registros da tabela com o comando:
``` bash
scala> jurosHiveDF.printSchema

scala> jurosHiveDF.show(5)
``` 
![Etapa 8](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_8_9_10.png?raw=true)

📢 ETAPA 9: SALVANDO NO FORMATO PARQUET

> Salvar o DataFrame jurosHiveDF no HDFS no diretório “/user/aluno/nome/data/save_juros” no formato parquet

Agora vamos salvar o "jurosHiveDF" no formato parquet no HDFScom o comando:
``` bash
scala> jurosHiveDF.write.parquet("/user/aluno/gabriel/data/save_juros")
``` 
![Etapa 9](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_11.png?raw=true)

Agora vamos consultar se o arquivo foi salvo no HDFS com o comando:
``` bash
$ hdfs dfs -ls /user/aluno/gabriel/data/save_juros
``` 
![Etapa 9.1](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_12.png?raw=true)


📢 ETAPA 10: VISUALIZANDO O PARQUET pelo Spark

> Criar o DataFrame jurosHDFS para ler o diretório do “save_juros” da etapa anterior
> Visualizar o Schema do jurosHDFS
> Mostrar os 5 primeiros registros do jurosHDFS
 
Pronto, agora na última etapa vamos criar um novo DF para ler o save_juros, logo após vamos visualizar o schema e exibir os primeiros 5 registros com os comandos:
``` bash
scala> val jurosHDFS = spark.read.load("/user/aluno/gabriel/data/save_juros")

scala> jurosHDFS.printSchema

scala> jurosHDFS.show(5)
``` 
![Etapa 10](https://github.com/gacarvalho/practice-spark-dataframe/blob/main/Spark%20-%20DataFrame/Exercicio_13_14_15.png?raw=true)
