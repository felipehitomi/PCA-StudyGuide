# System Architecture

[https://prometheus.io/docs/tutorials/getting_started/#basic-architecture-of-prometheus](https://prometheus.io/docs/tutorials/getting_started/#basic-architecture-of-prometheus)

The basic components of a Prometheus setup are:

- Prometheus Server (the server which scrapes and stores the metrics data).
- Targets to be scraped, for example an instrumented application that
exposes its metrics, or an exporter that exposes metrics of another
application.
- Alertmanager to raise alerts based on preset rules.

************************************************************************************************************************************************************************************De uma forma bem simples o que é a arquitetura do prometheus, ele basicamente pode coletar dados(metricas) e enviar alertas.************************************************************************************************************************************************************************************ 

![Untitled](System%20Architecture%201baaa00a02124112b0f8900dd9f41de7/Untitled.png)

**Client Libraries** 
Metrics do not typically magically spring forth from applications; someone has to add the instrumentation that produces them. This is where client libraries come in. With usually only two or three lines of code, you can both define a metric and add your desired instrumentation inline in code you control. This is referred to as **direct instrumentation**

Client libraries are available for all the major languages and runtimes. The Prometheus project provides official client libraries in Go, Python, Java/JVM, and Ruby. There are also a variety of third-party client libraries, such as for C#/.Net, Node.js, Haskell, Erlang, and Rust

*********************Alguem precisa colocar as metricas em codigo e para isso pode-se usar as bibliotecas de clientes.********************* 

Client libraries take care of all the nitty-gritty details such as thread-safety, bookkeeping, and producing the Prometheus text exposition format in response to HTTP requests. As metrics-based monitoring does not track individual events, client library memory usage does not increase the more events you have. Rather, memory is related to the number of metrics you have *********************************************************************************************************************O uso de memoria está associado  a  numero de métricas, não aos valores.********************************************************************************************************************* 

Client libraries are not restricted to outputting metrics in the Prometheus text format. Prometheus is an open ecosystem, and the same APIs used to feed the generation text format can be used to produce metrics in other formats or to feed into other instrumentation systems. Similarly, it is possible to take metrics from other instrumentation systems and plumb it into a Prometheus client library, if you haven’t quite converted everything to Prometheus instrumentation yet ***************************************************************************************Existe um padrão de formato para o prometheus, podendo voce utilizar ele ou outra forma e fazer um conversão.*************************************************************************************** 

**Exporters** 

Not all code you run is code that you can control or even have access to, and thus adding direct instrumentation isn’t really an option. For example, it is unlikely that operating system kernels will start outputting Prometheus-formatted metrics over HTTP anytime soon. Such software often has some interface through which you can access metrics. This might be an ad hoc format requiring custom parsing and handling ************************Alguns sistemas você não tem o codigo fonte, ou ele tem as métricas de uma forma que não compensa alterar. O Exporter faz essa conversão e gera uma rota para ocorer o “scrape”************************

An exporter is a piece of software that you deploy right beside the application you want to obtain metrics from. It takes in requests from Prometheus, gathers the required data from the application, transforms them into the correct format, and finally returns them in a response to Prometheus. You can think of an exporter as a small one-to-one proxy, converting data between the metrics interface of an application and the Prometheus exposition format ******Ele é uma casca a qual o prometheus pede informação, ele coleta, traduz e mostra para o prometheus.****** 

**Service Discovery**

[Service Discovery](Service%20Discovery%20e9cd935b8c1c4e669529bdeb2c87cce2.md)

**Scraping** 

Service discovery and relabelling give us a list of targets to be monitored. Now Prometheus needs to fetch the metrics. Prometheus does this by sending a HTTP request called a scrape. The response to the scrape is parsed and ingested into storage. Several useful metrics are also added in, such as if the scrape succeeded and how long it took. Scrapes happen regularly; usually you would configure it to happen every 10 to 60 seconds for each target  *********************Scrape é o ato do prometheus ir buscar as métricas que estavam na lista de targets e colocar as labels*********************

**Storage** 

Prometheus stores data locally in a custom database. Distributed systems are challenging to make reliable, so Prometheus does not attempt to do any form of clustering. In addition to reliability, this makes Prometheus easier to run. Over the years, storage has gone through a number of redesigns, with the storage system in Prometheus 2.0 being the third iteration. The storage system can handle ingesting millions of samples per second, making it possible to monitor thousands of machines with a single Prometheus server. The compression algorithm used can achieve 1.3 bytes per sample on real-world data. An SSD is recommended, but not strictly required ************************Salva em um banco tsdb local, eles fizeram algo que seria muito bom em olhar várias máquinas, assim não precisar ter mais de um prometheus, assim aumentando a velocidade. Compressão de dados alta para não precisar de muito disco.************************ 

**Dashboards** 

Prometheus has a number of HTTP APIs that allow you to both request raw data and evaluate PromQL queries. These can be used to produce graphs and dashboards. Out of the box, Prometheus provides the expression browser. It uses these APIs and is suitable for ad hoc querying and data exploration, but it is not a general dashboard system. It is recommended that you use Grafana for dashboards. It has a wide variety of features, including official support for Prometheus as a data source. Grafana supports talking to multiple Prometheus servers, even within a single dashboard panel ***************************************************************************************************************************************************A forma de ver dados no prometheus é muito ruim, usada só para uma pesquisa rápida ou afins, sendo necessário um outro visualizador como o Grafana.*************************************************************************************************************************************************** 

**Recording Rules and Alerts** 

Although PromQL and the storage engine are powerful and efficient, aggregating metrics from thousands of machines on the fly every time you render a graph can get a little laggy. Recording rules allow PromQL expressions to be evaluated on a regular basis and their results ingested into the storage engine. Alerting rules are another form of recording rules. They also evaluate PromQL expressions regularly, and any results from those expressions become alerts. Alerts are sent to the Alertmanager.  ***************************Record rules aumentam a velocidade, porque está por um periodo pré-definido olhando a query e guardando o valor. Os alertas são iguals, mas eles tem uma ação caso o que você  informou seja atingido.*************************** 

**Alert Management** 

The Alertmanager receives alerts from Prometheus servers and turns them into notifications. Notifications can include email, chat applications such as Slack, and services such as PagerDuty. The Alertmanager does more than blindly turn alerts into notifications on a one-toone basis. Related alerts can be aggregated into one notification, throttled to reduce pager storms,7 and different routing and notification outputs can be configured for each of your different teams. Alerts can also be silenced, perhaps to snooze an issue you are already aware of in advance when you know maintenance is scheduled ******Uma estrutura externa que recebe os alertas e faz as notificações, alem de ter outras regras que lidam com isso.****** 

The Alertmanager’s role stops at sending notifications; to manage human responses to incidents you should use services such as PagerDuty and ticketing systems ******************************Para receber respostas de humanos sobre o alerta deve-se utilizar  uma ferramenta tipo pagerduty ou algo de ticket.****************************** 

**Long-Term Storage**

Since Prometheus stores data only on the local machine, you are limited by how much disk space you can fit on that machine.8 While you usually care only about the most recent day or so worth of data, for long-term capacity planning a longer retention period is desirable. Prometheus does not offer a clustered storage solution to store data across multiple machines, but there are remote read and write APIs that allow other systems to hook in and take on this role. These allow PromQL queries to be transparently run against both local and remote data, ***************************************************Não existe opção de um cluster de armazenamento para o prometheus, se esse armazenamento prolongado é necessário pode-se utilizar o read-write remoto. é transparente ver local ou remoto.*************************************************** 

**What Prometheus Is Not**

Now that you have an idea of where Prometheus fits in the broader monitoring landscape and what its major components are, let’s look at some use cases for which Prometheus is not a particularly good choice. As a metrics-based system, Prometheus is not suitable for storing event logs or individual events. Nor is it the best choice for high cardinality data, such as email addresses or usernames. Prometheus is designed for operational monitoring, where small inaccuracies and race conditions due to factors like kernel scheduling and failed scrapes are a fact of life. Prometheus makes tradeoffs and prefers giving you data that is 99.9% correct over your monitoring breaking while waiting for perfect data. Thus in applications involving money or billing, Prometheus should be used with caution ******************************************************************não é algo pra logs, ou eventos, não é bom para alta cardinalidade e leva em conta que melhor ser 99% certo porem rapido do que 100% certo e devagar.******************************************************************