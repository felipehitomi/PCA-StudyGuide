# Exposition Format

Data: November 4, 2022 

---

Título:Exposition Format

---

Tópicos: [Devops](https://www.notion.so/Devops-a586a0555e794afeb8f763897448461b) [Prometheus](https://www.notion.so/Prometheus-22122ea9cfa44d359caee229f6acd7a0) [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978) 

---

Links Usados: [https://github.com/prometheus/docs/blob/main/content/docs/instrumenting/exposition_formats.md](https://github.com/prometheus/docs/blob/main/content/docs/instrumenting/exposition_formats.md)

---

Links a Usar:

---

Refs:

---

O formato que o prometheus espera que a metrica esteja exposta, algumas libs e exporters já vão exportar dessa forma. 

Hoje ele só aceita o formato text-based, antes ele já aceitou um chamado protobuf

O formato de texto que ele utiliza é  lido linha por linha, precisando de um \n no final e linhas em branco são desconsideradas. Essa linha precisa seguir alguns parametros, cada valor precisa ser separado por uma quantidade de espaços ou tabs, se não tiver eles são ser entendidos juntos. Espaços em branco antes ou depois são ignorados. 

Podemos fazer comentários e colocar palavras “chaves” depois desse  comentário que alteram como o prometheus vai mostrar esse campo. 

O # é um comentário que são ignorados no export das métricas, porem se utilizar `# HELP` e `# TYPE` o TYPE sendo necessário colocar o nome  da métrica, o que vier depois é utilizado como documentação para quem lê o /metrics. 

no caso do  TYPE é necessário colocar o nome da métrica e o tipo dela, se não for informado  será considerado  untyped. Ambos os dois só podem ser utilizados com 1 métrica só. 

essa linha precisa de alguns valores como 

```bash
metric_name [
  "{" label_name "=" `"` label_value `"` { "," label_name "=" `"` label_value `"` } [ "," ] "}"
] value [ timestamp ]
```

O nome da métrica = metric_name

Os nomes e valores das métricas (escapando) = label_name & label_value

O valor da métrica = value

O tempo em que isso ocorreu(lido no final mas no grafana mostra no começo) = timestamp

### Grouping

as métricas são mostradas como um grupo, acho que é quando se tem vários valores de labels e afins de uma métrica, ai elas são separada pelo HELP ou TYPE

é quando se agrupa todas as métricas e suas labels, porque sempre que se tem uma label diferente é uma nova linha. 

********************************************Histogram e summaries********************************************

Eles tem algumas particularidades como 

- The sample sum for a summary or histogram named `x` is given as a separate sample named `x_sum`.
- The sample count for a summary or histogram named `x` is given as a separate sample named `x_count`.
- Each quantile of a summary named `x` is given as a separate sample line with the same name `x` and a label `{quantile="y"}`.
- Each bucket count of a histogram named `x` is given as a separate sample line with the name `x_bucket` and a label `{le="y"}` (where `y` is the upper bound of the bucket).
- A histogram *must* have a bucket with `{le="+Inf"}`. Its value *must* be identical to the value of `x_count`.
- The buckets of a histogram and the quantiles of a summary must
appear in increasing numerical order of their label values (for the `le` or the `quantile` label, respectively).