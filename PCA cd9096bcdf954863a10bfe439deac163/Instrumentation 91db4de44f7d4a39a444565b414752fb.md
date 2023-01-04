# Instrumentation

**Data:** December 1, 2022 

---

**Título:** Instrumentation

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:**  [https://prometheus.io/docs/practices/instrumentation/](https://prometheus.io/docs/practices/instrumentation/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

Basicamente a ideia é que se instrumetalize tudo que puder, cada biblioteca, subsistema e afins

Instanciar as métricas no mesmo arquivo que você as utiliza, assim fica mais fácil de conseguir pelo alertar achar o codigo. 

3 Tipos de serviço 

**Online**

Serviço que outro humano ou máquina precisa acessar instantaneamente, algumas métricas comuns de um serviço http são

numero de queries, erros, latencia e etc. 

Seria ideal se pudesse monitorar do lado do client e do lado do server, assim facilita na hora de um debugg. 

**Offline**

Quando ninguem está esperano a resposta, pode ser realizado em lotes. 

é ideial colocar métricas sobre o caminho dos itens, para que consiga saber informações como timestamp em cada etapa. 

Metricas comuns seriam, quantos itens precisa fazer, quantos estão em processo, ultima vez que processou algo. 

**Batch Jobs**

Processos que acontecem e que não ficam ligados, executam e são desligados, necessitando usar o push gateway. 

Métricas comuns são, ultima vez que teve sucesso, quanto tempo demorou, quanto tempo o ultimo demorou. Lembrando que elas vão ser todas gauges porque são dinamicas. 

Se tiver um batch que demore mais que uns 15 min, é interessante fazer ele virar um offline 

**Sub Sistemas**

**Bibliotecas**

As bibliotecas deveriam disponibilizar algum tipo de métricas, e é interessante usar para captar error internos das mesmas. 

**Logging**

interessante pensar em  colocar métricas de count olhando para quantidade de vezes que uma linha de log apareceu, por exemplo um erro e etc. 

**Falhas**

Igual ao log, é interessante métrificas as falhas. 

**Atenções**

**Labels**

Pensar em horas de se  usar as labels

Não cria uma métrica nova se poderia usar uma label

O nome da métrica não deve ser gerado pelo codigo, use label

Tomar cuidado com a cardinalidade das labels

Comece sem labels e vá adicionando a necessidade

**Inner Loops**

Existem uma latencia do tempo que as métricas são lidas, então cuidado com essas alterações, c omo as syscalls de timestamp. 

**Missing Metrics**

Cuidado com métricas que não tenham valor, não faça elas sumirem, coloque  um valor de 0.