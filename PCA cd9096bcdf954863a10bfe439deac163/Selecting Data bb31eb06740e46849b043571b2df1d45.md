# Selecting Data

Data: November 9, 2022 

---

Título: Selecting Data

---

Tópicos: [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md) [Observabilidade](https://www.notion.so/Observabilidade-e434a18920744e7da17617bc3c96b978) 

---

Links Usados: [https://promlabs.com/blog/2020/07/02/selecting-data-in-promql](https://promlabs.com/blog/2020/07/02/selecting-data-in-promql)

---

Links a Usar:

---

Refs:

---

**********Instant Vector**********

é o ultimo valor do sample de cada resultado, tanto range como um outro instant, é chamado de instant vector porque ele devolve um vetor contendo um sample  por cada serie. 

**********Como funciona o matcher (fazer o select)********** 

se você colocar só o nome da métrica o prometheus vai trazer todos os valores dessa métrica. Ex:

`api_http_requests_total`

Mas pode também fazer a querry por label, ai é necessário abrir “chaves” e colocar o nome da label e o valor desejado. Ex

`api_http_requests_total{method="POST", handler="/api/widgets"}`

Pode-se utlizar os seguintes caracteres para alterar a forma da pesquisa, como:

- `=` igualdade
- `!=` para não igualdade
- `=~` para aplicar regex em toda a string
- `!~` para aplicar o regex negativo em toda a string

Ex:

`api_http_requests_total{method="POST", handler=~"/api/.*"}`

Mesmo o nome da métrica é uma label, então o __name__ é o nome da label e pode usar na querry. Ex:

`{__name__="api_http_requests_total"}`

 

É util quando se deseja fazer um regex em nomes das métricas como

`{__name__=~"api_.*"}`

Um instant olha valores até 5 minutos. Se você tiver algo que “sumiu” nesses 5 minutos o prometheus vai colocar uma marca “NaN” nele. Caso na hora de mostrar o resultado tiver uma marca “NaN” ele não vai mostrar. 

**************************Range Vector**************************

quando você quer delimitar um tempo que ele deve agregar os valores, exemplo de 5 em 5 minutos, de 30 em 30 minutos. 

`api_http_requests_total[5m]`

Sempre precisa colocar a unidade como, s (seconds), m (minutes), h (hours), d (days), w (weeks), y (years).

Você precisa transformar antes o valor do range para um instant, usando o rate é um jeito, mas ainda preciso entender um pouco melhor isso. 

`rate(api_http_requests_total[5m])`

**************Offset**************

Quando você precisa analisar os valores passados com os valores presentes, ai se usa o offset como exemplo

`rate(api_http_requests_total[5m] offset 1w)`

e abaixo calculando a diferença

`rate(api_http_requests_total[5m] offset 1w) - rate(api_http_requests_total[5m])`