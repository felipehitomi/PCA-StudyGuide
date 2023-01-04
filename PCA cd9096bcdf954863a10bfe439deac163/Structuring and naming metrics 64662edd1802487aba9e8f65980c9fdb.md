# Structuring and naming metrics

**Data:** November 29, 2022 

---

**Título:** Structuring and naming metrics

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** [https://prometheus.io/docs/practices/naming/](https://prometheus.io/docs/practices/naming/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

**Nome da métrica:**

Ele deve seguir o padrão de nomes do prometheus

É bom colocar uma palavra como prefixo que indique mais informações de onde ele vem, exemplo: prometheus_, http_, nomedaaplição_

Deve-se sempre usar as medidas de base(byte, segundos, metros)

Precisa ter um sufixo com as unidades, exemplo: _seconds, _bytes

**Labels:**

É interessante diferenciar algo dentro da métrica usando as labels, como uma operação = criar|deletar|atualizar

Sempre deve-se tomar cuidado com a cardinalidade das métricas, não usar para algo como nomes de usuário ou e-mails.