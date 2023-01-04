# Understand and Use Alertmanager

**Data:** December 13, 2022 

---

**Título:** Understand and Use Alertmanager

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** [https://prometheus.io/docs/alerting/latest/alertmanager/](https://prometheus.io/docs/alerting/latest/alertmanager/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

O Alertmanager cuida dos alertas que ele receber dos clientes, como server do prometheus. Ele toma conta de duplicações, agrupamento e roteamento entre eles, fazendo o envio para as integrações como e-mail, pagerduty e opsgenie, também toma conta de silenciamento e evitar flood. 

Alguns conceitos chave fazem parte do alertmanager como:

## Agrupamento(Grouping)

Quando você tem vários alertas da mesma base e não quer receber todos os alertas separados, ex: algo do cluster fez com que todas as apps saissem do ar, você não quer receber 20 alertas de cada aplicação e sim 1 alerta com as 20 aplicações dentro dele. 

É utilizada uma regra de roteamento(routing tree) que é configurada por aquivo, responsável por agrupar, fazer o controle de tempo e administrar quem recebe as notificações. 

## Inibição(Inhibition)

É quando não se quer receber alertas se algo “maior” aconteceu, ex se houve uma queda no seu cloud provider você não precisa receber alertas de que suas aplicações estão fora do ar. Também é configurado via arquivo.

## Silenciamento(Silences)

É quando você define politicas de silenciamento para um determinado tipo de alerta, exemplo se você vai realizar uma manutenção e sabe que o cluster ficará fora do ar, não é necessário receber alertas sobre o cluster ou a aplicação. 
Sempre vai ser usado  um matcher igual o routing  tree, eles são configurados na interface web do alertmanager. 

## Client behavior

Ações especiais para uso avançado

## High Availability

O alertmanager aceita uma flag, —cluster-* informando quantos servers você quer, lembrando que não é para colocar um load balancer entre o prometheus e os alermanagers e sim apontar o prometheus para uma lista de alermanagers