# Service Discovery

[https://thenewstack.io/observability-from-service-discovery-to-service-mesh/](https://thenewstack.io/observability-from-service-discovery-to-service-mesh/)

[https://medium.com/criteo-engineering/mixing-observability-with-service-discovery-2bb8909e8530](https://medium.com/criteo-engineering/mixing-observability-with-service-discovery-2bb8909e8530)

[https://docs.sysdig.com/en/docs/sysdig-monitor/monitoring-integrations/custom-integrations/collect-prometheus-metrics/enable-prometheus-native-service-discovery/](https://docs.sysdig.com/en/docs/sysdig-monitor/monitoring-integrations/custom-integrations/collect-prometheus-metrics/enable-prometheus-native-service-discovery/)

[https://www.udemy.com/course/prometheus-course/learn/lecture/20701886#overview](https://www.udemy.com/course/prometheus-course/learn/lecture/20701886#overview)

**Service Discovery**
Once you have all your applications instrumented and your exporters running,
Prometheus needs to know where they are. This is so Prometheus will know what is
meant to monitor, and be able to notice if something it is meant to be monitoring is
not responding. ************************************************************************************************************************************Como o prometheus vai descobrir o que monitorar e quando isso sair do ar************************************************************************************************************************************

With dynamic environments you cannot simply provide a list of
applications and exporters once, as it will get out of date. This is where service dis‐
covery comes in. ***Não tem como colocar todos os ips na mão, isso tudo vai mudar muito rapido***
You probably already have some database of your machines, applications, and what
they do. It might be inside Chef’s database, an inventory file for Ansible, based on
tags on your EC2 instance, in labels and annotations in Kubernetes, or maybe just
sitting in your documentation wiki.
Prometheus has integrations with many common service discovery mechanisms,
such as Kubernetes, EC2, and Consul. There is also a generic integration for those
whose setup is a little off the beaten path (see “File” on page 130).***tem mecanismos de discovery como k8s, e o consul***
This still leaves a problem though. Just because Prometheus has a list of machines and services doesn’t mean we know how they fit into your architecture. For example, you might be using the EC2 Name tag6 to indicate what application runs on a machine, whereas others might use a tag called app.
As every organisation does it slightly differently, Prometheus allows you to configure how metadata from service discovery is mapped to monitoring targets and their labels using relabelling. ***o relabel ajuda a mostrar como voce quer que seja descoberto.*** 

If your particular source isn’t already supported, you can use the file-based service discovery mechanism to hook it in. Labels are a key part of Prometheus, assigning target labels to targets allows them to be grouped and organised in ways that make sense to you. ***************************************************************************************Podemos usar uma forma de “discovery” como arquivo, mas que na verdade só seria um discovery se você tivesse algo automatizado fazendo a busca***************************************************************************************

Service discovery and the pull model allow all these views of the world to coexist, as each of your teams can run their own Prometheus with the target labels that make sense to them

**Service Discovery Mechanisms** 

Service discovery is designed to integrate with the machine and service databases that you already have. Out of the box, Prometheus 2.2.1 has support for Azure, Consul, DNS, EC2, GCE, OpenStack, File, Kubernetes, Marathon, Nerve, Serverset, and Triton service discovery in addition to the static discovery you have already seen. ************************************************************************O service discovery é uma forma automatica de se fazer consulta dos targets, e cada forma vai utilizar um jeito de fazer essa “coleta” de informações.************************************************************************ 

A good service discovery mechanism will provide you with metadata. Metadata is what you will convert into target labels, and generally the more metadata you have, the better.************************************************O metadata é que vai virar as labels que são utilizadas.************************************************ 

**Top-down Versus Bottom-up** 

There are two broad categories of service discovery mechanisms you will come across. Those where the service instances register with service discovery, such as Consul, are bottom-up. Those where instead the service discovery knows what should be there, such as EC2, are top-down. 

Both approaches are common. Top-down makes it easy for you to detect if something is meant to be running but isn’t. However, for bottom-up you would need a separate reconciliation process to ensure things are in sync, so that cases such as an application instance that stalls before it can register are caught. *********************************Parece que existem modos onde ele vai levar a informação e modos onde ele vai lá buscar as informações.********************************* 

**Static**

Static configuration in where targets are provided directly in the prometheus.yml.

**File**

File service discovery, usually referred to as file SD, does not use the network. Instead, it reads monitoring targets from files you provide on the local filesystem.

You can provide files in either JSON or YAML formats

![Untitled](Service%20Discovery%20e9cd935b8c1c4e669529bdeb2c87cce2/Untitled.png)

*********************a ordem do scrape, então sempre que você quer mudar algo antes do scrape você utilizar relabel_configs e depois metric_relabel_configs.*********************