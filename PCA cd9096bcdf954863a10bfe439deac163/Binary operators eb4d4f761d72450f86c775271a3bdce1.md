# Binary operators

**Data: November 23, 2022** 

---

**Título:** Binary operators

---

**Tópicos:  [PCA](../PCA%20cd9096bcdf954863a10bfe439deac163.md)** 

---

**Links Usados:** [https://prometheus.io/docs/prometheus/latest/querying/operators/](https://prometheus.io/docs/prometheus/latest/querying/operators/)

---

**Links a Usar:** 

---

**Refs:** 

---

**Conceitos para pesquisar depois:** 

**Conceitos para pesquisar depois:** 

- **Rates and Derivatives:**

$__interval

extrapolation

**Introduction to rates -** [https://www.youtube.com/watch?v=qGTYSAeLTOE](https://www.youtube.com/watch?v=qGTYSAeLTOE)

- **Aggregating over time:**

Scalar

**Vector matching**

Apdex Score

---

Operadores básicos de toda linguagem

Os **aritméticos**

- `+` (addition)
- `-` (subtraction)
- `*` (multiplication)
- `/` (division)
- `%` (modulo)
- `^` (power/exponentiation)

Os operadores binários respondem diferente para cada tipo

Entre dois scalares - Ele vai criar um novo scalar como resultado dos operadores

Entre um vetor e um scalar - ele cria um novo vetor fazendo a operação que foi solicitada, mas ele remove o nome da métrica

Entre um vetor e um vetor - um pouco mais confuso de quando se usar, mas ele vai fazer a operação entre o lado esquerdo e o seu matching element do lado direito, criando um novo vetor e tirando o nome da métrica, o que não tiver matching no lado direito não vai pro resultado. 

*o escalar é só um valor unico, tipo um int*

**Comparação**

- `==` (equal)
- `!=` (not-equal)
- `>` (greater-than)
- `<` (less-than)
- `>=` (greater-or-equal)
- `<=` (less-or-equal)

Tem as mesmas particularidades dependendo do que está se usando

Entre dois scalares, tem que usar o bool e vai gerar um outro scalar com 0(false) ou 1(true)

`1 == bool 1`

Entre um instante e um scalar, ele vai mostrar só os que seguem o que foi comparado, mas se voce mandar o bool ele vai mostrar eles como 0(false) se passar o bool o valor da métrica é dropado. 

Entre dois instant vector, ele vai fazer a mesma coisa do que o de cima, se não for ele vai dropar mas se colocar o bool ele vai mostrar como false. 

E tem por ultimo o **logico**

- `and` (intersection)
- `or` (union)
- `unless` (complement)

vetor 1 and vetor 2 vai resultar em um vetor que tenha as labels em comum exatamente os outros elementos são dropados

vetor 1 or vetor 2 vai resultar num vetor “somando” os dois tem todos os originais do 1 e os elementos que não tiveram match nas labels

Vetor1 unless vetor2 elementos do 1 que não tem matching no vetor 2. todos os que derem match são dropados.