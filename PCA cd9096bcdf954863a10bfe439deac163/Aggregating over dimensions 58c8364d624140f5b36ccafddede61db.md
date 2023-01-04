# Aggregating over dimensions

**Data:**  November 23, 2022 

---

**Título:** Aggregating over dimensions

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Devops](https://www.notion.so/Devops-a586a0555e794afeb8f763897448461b) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** [https://prometheus.io/docs/prometheus/latest/querying/operators/#aggregation-operators](https://prometheus.io/docs/prometheus/latest/querying/operators/#aggregation-operators)

---

**Links a Usar:** 

---

**Refs:** 

---

********************************Conceitos para pesquisar depois:********************************

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

Quando se faz alguma operação sobre a time series, exemplo:

- `sum` (calculate sum over dimensions)
- `min` (select minimum over dimensions)
- `max` (select maximum over dimensions)
- `avg` (calculate the average over dimensions)
- `group` (all values in the resulting vector are 1)
- `stddev` (calculate population standard deviation over dimensions)
- `stdvar` (calculate population standard variance over dimensions)
- `count` (count number of elements in the vector)
- `count_values` (count number of elements with the same value)
- `bottomk` (smallest k elements by sample value)
- `topk` (largest k elements by sample value)
- `quantile` (calculate φ-quantile (0 ≤ φ ≤ 1) over dimensions)

  

É aqui que se pode usar o `without` e o `by` para separar as labels. 

A sintaxe fica assim:

```
<aggr-op> [without|by (<label list>)] ([parameter,] <vector expression>)

```

ou 

```
<aggr-op>([parameter,] <vector expression>) [without|by (<label list>)]

```

essa label list são as labels sem aspas e separadas por virgula. 

O `without` remove as labels que foram listadas e o `by` faz o contrario, selecionando só essas labels.