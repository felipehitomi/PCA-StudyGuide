# Exporters

**Data:**  December 2, 2022 

---

**Título:** Exporters

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:**  [https://prometheus.io/docs/instrumenting/exporters/](https://prometheus.io/docs/instrumenting/exporters/)

[https://alanstorm.com/what-are-prometheus-exporters/](https://alanstorm.com/what-are-prometheus-exporters/)

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

Quando você não tem possibilidade de instrumentalizar um código, quando é algo fechado ou algo de terceiros ( ex: linux) 

Esses exporters são as vezes mantidos pelo Prometheus marcados como official. 

Alguns tipos de exporters são:

- Databases
- Hardware
- CI
- Mensageria
- Storage
- HTTP
- Api’s
- Logging
- Outros software’s (Docker)

![Untitled](Exporters%20b932e7c186a74cb7b6736c2a8ed68b8a/Untitled.png)

Um exporter pode ser considerado um “tradutor” que vai olhar as métricas em um formato e expor essas métricas em um formato adequado para o Prometheus. 

Pode-se usar uma linguagem tipo go, que já tem um cliente de exportação, e ele olhar as métricas e exportar.