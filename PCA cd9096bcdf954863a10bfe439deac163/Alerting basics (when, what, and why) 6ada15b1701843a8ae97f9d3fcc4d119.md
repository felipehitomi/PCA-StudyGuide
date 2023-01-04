# Alerting basics (when, what, and why)

**Data:**  December 14, 2022 

---

**Título:** Alerting basics (when, what, and why)

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** [https://www.oreilly.com/library/view/effective-monitoring-and/9781449333515/ch01.html](https://www.oreilly.com/library/view/effective-monitoring-and/9781449333515/ch01.html)
[https://prometheus.io/docs/practices/alerting/](https://prometheus.io/docs/practices/alerting/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

Com a forma moderna de como criamos software, ter uma base de monitoria solida é essencial para conseguir resolver problemas. E ter performance em tempo real, granularidade de dados, interpretação dos dados é essencial, não estamos mais no tempo que tinhamos poucos lugares para procurar o erro. 

Com monitoria você consegue pegar inconsistencias antes delas se tornarem problemas, garantindo a alta disponibiidade e qualidade do serviço. Outro beneficio é te dar uma visão do passado, presente e futuro, criando insights de automação da infraestrutura. 

Alerta é a capacidade de um sistema de monitoria notificar os operadores de eventos que alterem o estado. A notificação é refenciada ao alerta como uma mensagem em algumas formas: SMS, E-mail, Slack, ligação. Assim o alerta passa para uma parte responsável pelo evento, podendo tambem ser enviado a um sistema de tickets como uma Issue. 

Um alerta pode ser util em detecção antecipada de problemas, disponibilidade e performance. 

# Dicas sobre alertas

Mantenha alertas simples, alerte quando tiver um sintoma, tenha consoles que ajude a achar causas, e não tenha paginas que não há o que fazer. 

Manter o alerta simples, que ele avise impactor no que o usuário final vai sentir e não tentar alertar sobre tudo o que pode acontecer. E ter como saber o que está causando a falha. 

## Sistemas online

Alertar latencia e errors o mais alto na stack quanto possivel, basicamente é olhar latencia e erros que são visiveis ao usuário ou que possam estar envolvidos com perca de dinheiro. 

Cuidado para um erro em um trafego baixo não ser “engolido” por um de trafego alto. 

## Sistemas offline

Alertar quanto tempo demora para executar, e só alertar caso cause impacto ao usuário. 

## Batch jobs

Aqui é olhar falhas que causem impacto ao usuário, geralmente umas 2 vezes em que a execução não rodar. Caso seja algo mais importante ao inves de alertar com 1 falha deve-se diminuir o tempo entre execuções. 

## Capacity

Quando se está chegando ao limite de capacidade por mais que isso não causa impacto é necessário uma intervenção humana, então deve-se alertar. 

## Metamonitoria

é importante saber se os sistemas de monitoria estão funcionando corretamente, ter alertas sobre o prometheus, alertmanager, pushgateways ajudam a evitar problemas. 

Sempre que possível tentar um teste blackbox, testar todo o caminho de alerta, não só o ultimo da cadeia. Usando o whitebox e o blackbox ajudam a evitar erros que podem acontecer.