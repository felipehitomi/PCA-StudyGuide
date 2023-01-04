# Push vs Pull

[https://giedrius.blog/2019/05/11/push-vs-pull-in-monitoring-systems/](https://giedrius.blog/2019/05/11/push-vs-pull-in-monitoring-systems/)

[https://www.scribd.com/document/403518619/Application-Monitoring-with-Prometheus-intro-practical-tips-and-Adform-s-experience](https://www.scribd.com/document/403518619/Application-Monitoring-with-Prometheus-intro-practical-tips-and-Adform-s-experience)

[https://www.alibabacloud.com/blog/pull-or-push-how-to-select-monitoring-systems_599007](https://www.alibabacloud.com/blog/pull-or-push-how-to-select-monitoring-systems_599007)

[https://prometheus.io/blog/2016/07/23/pull-does-not-scale-or-does-it/](https://prometheus.io/blog/2016/07/23/pull-does-not-scale-or-does-it/)

[https://thenewstack.io/exploring-prometheus-use-cases-brian-brazil/](https://thenewstack.io/exploring-prometheus-use-cases-brian-brazil/)

[https://steve-mushero.medium.com/push-vs-pull-configs-for-monitoring-c541eaf9e927](https://steve-mushero.medium.com/push-vs-pull-configs-for-monitoring-c541eaf9e927)

## In Favor Of Push: Might Potentially Be More Performant

Push methods typically use UDP whereas pull methods are based on TCP 
(HTTP). What this means is that we could potentially push metrics more 
performantly than pull them. This is due to the fact that there is way 
less overhead for managing UDP connections. For example, there is no 
need to check if the message that you have sent to your peer has been 
actually received and in the correct order.

Metrics get pushed (usually via UDP) into the system or they get pulled (usually via HTTP).

The push method is used in systems such as [Graphite](https://graphiteapp.org/) whereas the pull method is used by monitoring systems like [Prometheus](https://prometheus.io/).

When pulling the data we can be sure of the authenticity of the data since the server itself is which initiates the connection, easier to plan the capacity of pull-based systems since the exact targets from which metric data will be gathered is known in advance ***Quando você está fazendo o pulling, você sabe de onde está buscando as informações, então consegue limitar***

on push-based systems, any kind of system can push to the metric gathering server. This could be fixed by using a whitelist of servers from which to accept data but most push-based systems do not support that ***Em sistemas de push, você precisa ter alguma forma de limitar o recebimento, utilizando por exemplo sistas  de aceitação, o que alguns não possuem esse suporte.*** 

Push: Easier To Implement Replication To Different Ingestion Points

Since it is all initiated by the client itself it becomes easier to replicate the same traffic to different servers. You just need to transmit it to more than one target IP address. ***É realmente mais fácil um sistema de push enviar para 2 ip’s, do que fazer 2 sistemas de pull ir buscar.*** 

Also, consider the fact that all of the receivers will get the same exact data. If you would spin up two different instances of Prometheus (which uses the HTTP pull method) then they most likely will not have the same exact data. ***Você tem algumas diferenças quando se tem o sistema de pull, porque o time stamp é diferente, e a hora que coletar pode ter outros dados.***

**In Favor Of Pull: Easier to Encrypt The Traffic**

It is very easy to put a TLS terminating reverse proxy in front of an ordinary HTTP server which serves metrics, and we could even use something like letsencrypt to automatically get a certificate if it is a public facing system or a certificate from a private CA that everyone on your intranet trusts ***É fácil colocar um servidor tls na frente ou colocar certificado.*** 

**In Favor Of Push: Easy To Model Shortlived Batch-Jobs**

In the push method, the client itself pushes the metrics to the server. On the other hand, in the pull method, the server periodically probes the clients and gathers their metrics. In Prometheus, this is called the scrape period. This has a (painful) result – if the client does not survive for longer than the period, the metrics are lost

***No push tem a vantagem de o serviço executar, mandar as métricas e depois parar, já no pull ele precisa ficar vivo tempo suficiente. Mas o prometheus já tem uma resposta para isso, que é o push gateway***

**In Favor Of Pull: Easier To Retrieve Data On Demand (And Debug)**

Having a pull method on top of TCP (HTTP) means that it is very easy to retrieve data on demand and debug the problems. Especially, if the metrics data is human-readable and easily understandable like the format used by Prometheus.

This gives you the opportunity to easily distinguish between the errors on the client side and the server side. In the push method, our hands would be kind of tied behind our back because if we were not receiving any metrics then it means one of two things:

- there is something wrong with the network
there is something wrong with the client

***é muito fácil ir pegar as métricas em um sistema de pull, pq elas estão sempre expostas lá, em um sistema de push voce tem que esperar que está sendo exposto*** 

**In Favor Of Push: Might Potentially Be More Performant**

Push methods typically use UDP whereas pull methods are based on TCP (HTTP). What this means is that we could potentially push metrics more performantly than pull them. This is due to the fact that there is way less overhead for managing UDP connections. For example, there is no need to check if the message that you have sent to your peer has been actually received and in the correct order.

***poderia ser mais performatico porem não é o que se ve muito hoje em dia, o tcp está bem rapido e performatico*** 

**Conclusion**

Both of these two models have their pros and cons. However, it seems that the pull-based model won since it offers just a little bit more reliability (especially when talking about very large scale deployments) and that it needs just a bit less number of workarounds to satisfy all of the possible metrics gathering use cases.

***parece que o modelo de pull ficou mais utilizado pela forma como é se aplicar ele, é mais fácil utilizar um server expondo as métricas do que lidar com um server enviando todo tempo, e mais facil ir em quem puxa e limitar o que puxa, do que ir tem todos os que enviam e ir cortando um a um.***