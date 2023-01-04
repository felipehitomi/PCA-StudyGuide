# Rates and Derivatives

**Data:** November 12, 2022 

---

**Título:**Rates and Derivatives

---

**Tópicos:** [Prometheus](https://www.notion.so/Prometheus-22122ea9cfa44d359caee229f6acd7a0) [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978) 

---

**Links Usados:**[https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/](https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/)

[https://prometheus.io/docs/prometheus/latest/querying/functions/#deriv](https://prometheus.io/docs/prometheus/latest/querying/functions/#deriv)

[https://prometheus.io/docs/prometheus/latest/querying/functions/#rate](https://prometheus.io/docs/prometheus/latest/querying/functions/#rate)

---

**Links a Usar:**

---

**Refs:** Documentação do prometheus

---

**Conceitos para pesquisar depois:** 

- **Rates and Derivatives:**

$__interval

extrapolation

**Introduction to rates -** [https://www.youtube.com/watch?v=qGTYSAeLTOE](https://www.youtube.com/watch?v=qGTYSAeLTOE)

- **Aggregating over time:**

Scalar

**Vector matching**

Apdex Score

---

Predição

A média que algo está aumentando por segundo

Parece que o range é quando se olha algo em um periodo de  tempo, então se tem os valores que ocorreram em por exemplo em 1 minuto, e o instant é quando  se olha só o valor do momento da querry. 

Ai o rate parece que é quando se faz um calculo entre 2 pontos e deve-se olhar o quanto ele subiu. Quando se pensa em quanto tempo vamos colocar precisa se tomar cuidado, porque se colocar de menos vai sempre ter uns spikes, e se colocar demais fica algo tão “macio” que não se vê os spikes. 

Uma dica é colocar vários valores no grafana para se encontrar o ideal. g

Basicamente o rate calcula a diferença do valor que ocorreu no determinado tempo. Por exemplo, quanto mudou em 35 s, mas ele não calcula só o primeio e o ultimo valor, pra isso se usa o irate()

![[https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/](https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/)](Rates%20and%20Derivatives%20b5dd80e4dbee4eefa61b697fe7c2c201/Untitled.png)

[https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/](https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/)

Ele é bom para métricas que estão sempre aumentando, mas ele se ajusta para resets, então deve-se usar em counter não em gauge. 

<aside>
⚠️ como o rate() se adequa a resets, deve-se usar ele primeiro caso você deseja agregar outras formulas junto.

</aside>

quando ele percebe um reset, ele soma o valor atual com o ultimo e calcula com ele. 

O rate() tenta extrapolar um resultado caso tenha um valor missing ou se o scraping falhou, temos que lembrar que isso pode acontecer porque o alinhamento entre o tempo da querry e o tempo de scraping podem ser diferentes e entre várias coisas. 

Essa função é boa para predição, spikes e alertas. 

Ele tambem faz o aggregation que é quando se usa o `by`tipo `rate(foo) by (bar)` 

Pode ser usado também para calculo de SLO como o google faz abaixo

![[https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/](https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/)](Rates%20and%20Derivatives%20b5dd80e4dbee4eefa61b697fe7c2c201/Untitled%201.png)

[https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/](https://www.metricfire.com/blog/understanding-the-prometheus-rate-function/)

basicamente ele olha tudo que não é 500 e divide pelo total, então se por exemplo de 10 requisições 9 não são 500 a conta ficaria

9/10 = 0.9 e esse valor abaixo é que estaria abaixo da entrega. 

Derivativo tambem parece uma forma de predição, usada em range vector tambem.