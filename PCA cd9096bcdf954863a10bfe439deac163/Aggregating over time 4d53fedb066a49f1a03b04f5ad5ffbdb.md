# Aggregating over time

**Data:** November 16, 2022 

---

**Título:** Aggregating over time

---

**Tópicos: [Devops](https://www.notion.so/Devops-a586a0555e794afeb8f763897448461b) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978) [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md)** 

---

**Links Usados:** [https://prometheus.io/docs/prometheus/latest/querying/functions/#aggregation_over_time](https://prometheus.io/docs/prometheus/latest/querying/functions/#aggregation_over_time)

---

**Links a Usar:** 

---

**Refs:** 

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

São funções que fazem uma agregação das series no range de vetor e retorna um instant vector. Mas sobre um tempo especifico

Exemplo:

- `avg_over_time(range-vector)`: the average value of all points in the specified interval.
- `min_over_time(range-vector)`: the minimum value of all points in the specified interval.
- `max_over_time(range-vector)`: the maximum value of all points in the specified interval.
- `sum_over_time(range-vector)`: the sum of all values in the specified interval.
- `count_over_time(range-vector)`: the count of all values in the specified interval.
- `quantile_over_time(scalar, range-vector)`: the φ-quantile (0 ≤ φ ≤ 1) of the values in the specified interval.
- `stddev_over_time(range-vector)`: the population standard deviation of the values in the specified interval.
- `stdvar_over_time(range-vector)`: the population standard variance of the values in the specified interval.
- `last_over_time(range-vector)`: the most recent point value in specified interval.
- `present_over_time(range-vector)`: the value 1 for any series in the specified interval.