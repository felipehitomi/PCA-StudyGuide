# Dashboarding basics

**Data:** December 14, 2022 

---

**Título:** Dashboarding basics

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** 

[https://prometheus.io/docs/practices/consoles/](https://prometheus.io/docs/practices/consoles/)

[https://prometheus.io/docs/visualization/grafana/](https://prometheus.io/docs/visualization/grafana/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

É tentador ter muita informação nos dashboards, porem essa quantidade pode confundir até um expert no sistema

Pensar no que é mais provavel de falhar, dividir por serviço

Algumas Dicas:

- Não ter mais que 5 graficos no console
- Não ter mais que 5 linhas no grafico, pode ser mais se for stacked/area
- quando usar template não usar mais que 20~30 entradas no lado direito
- tirar o que quase nunca usa
- talvez dividir por area o mesmo serviço, dev e ops

Um sistema a parte para visulizar os dashs é o granfana, prometheus é um data source no grafana.