# Data Model and Labels

Data: November 3, 2022 

---

Título: Data Model and Labels

---

Tópicos: [Prometheus](https://www.notion.so/Prometheus-22122ea9cfa44d359caee229f6acd7a0) [Devops](https://www.notion.so/Devops-a586a0555e794afeb8f763897448461b) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978) 

---

Links Usados:[https://prometheus.io/docs/concepts/data_model/](https://prometheus.io/docs/concepts/data_model/)

---

Links a Usar:

---

Refs: Documentação do Prometheus

---

A forma como o prometheus guarda os dados é em uma unidade chamada time series, que são sequencias de valores de tempo (timestamp) que pertencem a mesma métrica ou  “label”. O prometheus pode gerar alguns time series resultante de queries. 

## Métricas

A métrica precisa de um  nome que é um texto que deve explicar o que a métrica significa, esse texto deve seguir o padrão de  regex [a-zA-Z_:][a-zA-z0-9_:]*

<aside>
💡 os : são usados em “recording rules” não deve ser usado em instrumentalização ou exporters.

</aside>

## Labels

As labels são valores extras que podem ser colocados nas métricas, quando se colocar esse valor extra ele cria um novo time series, então um tipo de labels dão o aspecto dimensional. pode-se fazer pesquisa por essas labels. Elas seguem o reges [a-zA-Z_][a-zA-Z-0-9_]*

<aside>
💡 quando se vê __ no começo de uma label é que é usada internamente

</aside>

## Samples

Samples são os valores propriamente ditos que as métricas tem, podendo ser:

- um valor float64
- um timestamp de millisecond-precision

## Notation

A construção inteira de uma métrica com label fica igual abaixo

<metric name>{<label name>=<label value> …} <sample>