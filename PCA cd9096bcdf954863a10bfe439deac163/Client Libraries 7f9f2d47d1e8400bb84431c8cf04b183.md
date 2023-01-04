# Client Libraries

**Data:** November 29, 2022 

---

**Título:** Client Libraries

---

**Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978)** 

---

**Links Usados:** [https://prometheus.io/docs/instrumenting/clientlibs/](https://prometheus.io/docs/instrumenting/clientlibs/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

---

É chamado tambem de instumentalização, é um codigo colocado no seu codigo para gerar métrica no padrão do prometheus.

Existem em várias linguagem oficiais como :

- Go
- Java or Scala
- Python
- Ruby
- Rus

E não oficiais como :

- Bash
C
C++
Common Lisp
Dart
Elixir
Erlang
Haskell
Lua for Nginx
Lua for Tarantool
.NET / C#
Node.js
OCaml
Perl
PHP
R

Quando o prometheus vai fazer o scrape a biblioteca vai gerar as métricas e enviar para o servidor expor. 

Se não existir uma biblioteca voce pode criar uma se seguir o padrão que o prometheus espera receber.