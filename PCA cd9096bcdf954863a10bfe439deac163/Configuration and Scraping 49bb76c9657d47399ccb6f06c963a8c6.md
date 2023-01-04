# Configuration and Scraping

[https://prometheus.io/docs/prometheus/latest/configuration/configuration/](https://prometheus.io/docs/prometheus/latest/configuration/configuration/)

O prometheus tem 2 tips de configuração, a do sistema e a dos scrapes. A do sistema você manda por linha de comando quando sobe a aplicação ou provavelmente tem algo no configmap do k8s. A de scrape é  um arquivo chamado prometheus.yml onde se coloca as configs de scrape, como os alvos e como será feita a coleta, tambem se coloca sobre service discovery. 

para ver todas as opções de linha de comando usar 

```bash
prometheus -h
```

pode-se fazer um reload das config usando o sighup pro processo ou enviando um http pro /-/reload

Dá pra tambem passar qual arquivo voce quer usar passando a flag  ao lado. 

```bash
--config.file
```

Esse arquivo tem uma seção global que vale para todas as outras config que virão posteriormente, caso você não tenha colocado um novo valor lá. 

os valores mais importantes são:

- scrape_interval - é de quanto em quanto tempo ele vai olhar para o alvo e vai ler o /metrics
- scrape_timeout - é o tempo que vai demorar para ele entender que deu um timeout
- evaluation_interval - o mesmo do scrape mas para regras(rules)
- external_labels - uma label que vai ser colocada quando ele vai se comunicar com sistemas externos
- scrape_config - onde voce vai colocar as informações de scrape, os targets e etc.
- remote_write - quando você precisa mandar os dados coletados para um outro prometheus.

## Scraping

A configuração de scraping basicamente são os “alvos” e como fazer o scrape deles. 

geralmente existe uma config de scrape por job, lembrando que voce pode colocar o valor dele estatico, nunca mudando, ou dinamico, com várias formas de service discovery. 

E o relabel faz o gerenciamento de etiquetas.