# Understanding Prometheus Limitations

Data: November 2, 2022 

---

Titulo: Understanding Prometheus Limitations

---

Tópicos: [Devops](https://www.notion.so/Devops-a586a0555e794afeb8f763897448461b) [Prometheus](https://www.notion.so/Prometheus-22122ea9cfa44d359caee229f6acd7a0) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978) 

---

Links Usados:

[https://www.dynatrace.com/news/blog/what-is-prometheus/](https://www.dynatrace.com/news/blog/what-is-prometheus/)

---

Links a Usar:

---

Refs:

---

Quando se vai instalar um prometheus existem algumas limitações que se deve considerar por exemplo:

- segurança: não existe uma autenticação ou proteção por tls nativa, você precisa configurar de alguma forma. Você entrega isso para um NGINX.
- controle de acesso: depois de ter acesso ao prometheus voce consegue ver qualquer métrica que tenha nele, não existe uma forma me permissão.
- escalabilidade: ele não é de forma fácil escalável horizontalmente(ou seja, mais máquinas) é só em nível vertical (mais recursos) se pode perceber que está lento quando for dar um refresh  em um board do grafana.

<aside>
💡 1 milhão de métricas consomem aproximadamente 100GB de RAM

</aside>

Pode-se usar vários prometheus  e vários grafana, assim se expande e se protege os dados.