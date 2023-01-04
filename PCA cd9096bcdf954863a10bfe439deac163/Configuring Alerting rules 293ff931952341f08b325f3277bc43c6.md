# Configuring Alerting rules

**Data:**  December 11, 2022 

---

**Título:** Configuring Alerting rules

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** [https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

Regras de alerta deixam quem você defina condições para alertas baseado em expressões PromQL do prometheus. 

# Definindo regras de alerta

Segue o mesmo padrão das **********recording rules,********** pode-se colocar em arquivo como abaixo. 

![Untitled](Configuring%20Alerting%20rules%20293ff931952341f08b325f3277bc43c6/Untitled.png)

O ****for**** é opcional e ele válida de quando em quanto tempo o prometheus vai analisar esse alerta. No caso acima de 10 em 10 minutos, caso ele valide um cenário de alerta vai deixar em *******pending******* o alerta e analisar de novo em 10 minutos, se se manter ai o estado no alerta é ******firing.******

Pode-se colocar uma *****label***** no alerta, caso tenha conflitos de labels tem uma sobreescrição. ***Annotations*** são informações extras armazenas a longo prazo, como descrição e uma url de runbook. Tanto as labels como as annotations podem usar templates. 

# Templates

A labels e anotations pode ser usados com tempaltes, a variável $label mantem a estrutura chave/valor da instancia e $externalLabels guarda valores externos da instancia. 

![Untitled](Configuring%20Alerting%20rules%20293ff931952341f08b325f3277bc43c6/Untitled%201.png)