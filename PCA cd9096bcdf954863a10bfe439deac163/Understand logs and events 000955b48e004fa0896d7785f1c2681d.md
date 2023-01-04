# Understand logs and events

[https://medium.com/dzerolabs/observability-journey-understanding-logs-events-traces-and-spans-836524d63172](https://medium.com/dzerolabs/observability-journey-understanding-logs-events-traces-and-spans-836524d63172)

[https://docs.google.com/presentation/d/1GIvoN2nmXM9s2_7SJ2FWceDAG6XBvXTTTIo5FNfUNeQ/edit#slide=id.p](https://docs.google.com/presentation/d/1GIvoN2nmXM9s2_7SJ2FWceDAG6XBvXTTTIo5FNfUNeQ/edit#slide=id.p)

**Logs**

Logs are human-readable flat text files that are used by developers to capture useful data. Logs messages occur at a single point in time (though not necessarily at every point in time).

Unfortunately, log formats aren’t standardized across languages or frameworks, and they can be hard to parse and challenging to query. It’s also hard to group related logs together.

***É um texto que o programa solta em momentos variados com informações importantes, não precisa ser a cada ponto no tempo. Os logs não tem um padrão por cada linguagem, framework, sistema, o que dificulta agrupar-los.*** 

**Events**

Events are structured logs. They follow a standardized format (JSON), and are way easier to query.

**Behold a sample log:**

![https://miro.medium.com/max/700/1*dMx03t3s39tTv1BN4xZNJg.png](https://miro.medium.com/max/700/1*dMx03t3s39tTv1BN4xZNJg.png)

**And its Event counterpart:**

![https://miro.medium.com/max/700/1*nS68QO_uI-VQchj5b4bCJg.png](https://miro.medium.com/max/700/1*nS68QO_uI-VQchj5b4bCJg.png)

Source: [The Path from Logs to Traces,](https://docs.google.com/presentation/d/1GIvoN2nmXM9s2_7SJ2FWceDAG6XBvXTTTIo5FNfUNeQ/edit?usp=sharing) by [Alex Vondrak](https://www.linkedin.com/in/ajvondrak)

***Se considera um evento quando se tem um tratamento encima do log, colocando ele em formato JSON.***