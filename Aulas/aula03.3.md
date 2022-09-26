# 3.3 Análise Sintática Ascendente

Análise sintática ascendente (_bottom-up_) é um tipo de análise em que 
a construção da árvore sintática para uma cadeia w
começa pelas folhas e prossegue em direção à raiz.
```
	 S
	^^^
	|||
	|||
	 w
```
Seja uma gramática G = (N,T,P,S).
Se a cadeia de entrada w for válida (uma sentença de L(G)), 
ela é _reduzida_, em um ou mais passos, ao símbolo inicial da gramática (S).
O processo de _redução_ é inverso ao de derivação:

- uma subcadeia ```β``` de uma forma sentencial ```αβγ``` 
que coincide com o lado direito de alguma regra de produção ```A → β``` 
é substituída pelo não-terminal A à esquerda da regra de produção, 
obtendo-se uma nova forma sentencial ```αAγ```.

- a subcadeia ```β``` é o redutendo (_handle_) da forma sentencial ```αβγ```.

## Algoritmo de Análise Ascendente

### Funcionamento Básico

- Adota-se como o valor inicial de ```α``` a cadeia de entrada.

- Procura-se decompor ```α``` de tal maneira que ```α = βX1X2...Xnγ```, 
e exista uma produção da forma X → X1X2...Xn. 
Caso isto seja possível, adota-se a nova cadeia ```α = βXγ```, 
associando-se a essa ocorrência do não-terminal X uma árvore cuja raiz tem rótulo X 
e cujas subárvores diretas são as árvores que estavam associadas às ocorrências de X1X2...Xn 
que foram substituídas. 
Se Xi é um símbolo terminal, então a árvore associada será uma folha de rótulo Xi .

- O passo 2 é repetido até que o valor de α seja o símbolo inicial da gramática (S).

### Observações

Na prática, o algoritmo de análise sintática não precisa, em geral, 
conhecer a cadeia _α_ para decidir qual a próxima redução. 

É suficiente conhecer uma parte inicial ```α′``` de ```α``` e, 
quando necessário, novos símbolos serão lidos, estendendo ```α′```.

#### Exemplo.

```G1 = ({E,T,F}, {a,b,+,*,(,)}, P1, E)```
```
P1:	E ::= E + T | T			
	T ::= T * F | F
	F ::= a | b | (E)
```

Seja a cadeia (sentença) __w = a + b * a__ 
e as reduções sucessivas possíveis indicadas de (a) até (i), com os redutendos em negrito:

(a) **a** + b * a

(b) **F** + b * a

(c) **T** + b * a

(d) E + **b** * a

(e) E + **F** * a

(f) E + T * **a**

(g) E + **T * F**

(h) **E + T**

(i) E


Se as formas sentenciais de (a) a (i) forem lidas de baixo para cima,
obteremos a **derivação direita** da cadeia de entrada w.

```
E  ⇒  E + T       (h)
   ⇒  E + T * F   (g)
   ⇒  E + T * a   (f)
   ⇒  E + F * a  ⇒  E + b * a  ⇒ T + b * a  (e)(d)(c)
   ⇒  F + b * a   (b)
   ⇒  a + b * a
```

### Problemas Básicos da Análise Ascendente

O algoritmo de análise sintática deve aplicar a redução ao redutendo de uma forma sentencial direita.

#### A. Identificação da parte da cadeia a ser reduzida (redutendo)

Seja a forma sentencial  ```E + T * a``` obtida durante a análise sintática para uma cadeia w.

Podemos reduzir: 

(i)   a  para F, 
   
(ii)  T para E  ou 
   
(iii) E + T para E.

A depender da escolha, não é possível obter uma árvore sintática 
para a cadeia cuja raiz é o símbolo inicial da gramática.
Esta é uma situação indesejável e o algoritmo de análise nunca devem escolher reduções erradas.

#### B. Identificação da regra de produção que deve ser usada na redução

Se a gramática usada possui duas produções:

```(1) A → β```    e    ```(2) B → β```

e se o redutendo é ```β```, 

então deve existir alguma maneira de decidir qual das duas produções deve ser usada.


## Análise LR(k)

Estilo genérico de análise ascendente que segue a filosofia _shift-reduce_ (desloca-reduz). 
As operações de deslocamento e redução são realizadas em uma pilha.

### Analisadores LR(k)

L - left-to-right scanning of the input.

R - constructing the rightmost derivation in reverse.

k - número de símbolos de entrada (lookahead) usados para decidir sobre a próxima ação.


### Vantagens do método LR

- Analisadores são mais eficientes.

- A classe de gramáticas analisáveis é mais genérica.

- Inclui a classe LL(k).

- Detecção de erros eficiente.


### Desvantagens do Método LR

É muito trabalhoso construir a mão um analisador ascendente LR(k) para uma gramática qualquer.

### Método de _shift-reduce_

__FIGURA__:
entrada
saída
pilha de estados
        ...
        e0
 tabela LR
                                                           

#### Elementos

- analisador LR
- entrada
- pilha de estados
- tabela LR

- O estado no topo da pilha é o estado corrente do analisador e contém informações que resumem o que está abaixo dele na pilha  (p.e., quanto de um redutendo já foi analisado).

- O analisador consulta o estado no topo da pilha e o próximo símbolo (da entrada ou símbolo reduzido) para decidir qual a próxima ação. 

- O conjunto de estados do analisador é obtido a partir da gramática livre de contexto da linguagem.

- As ações ficam na tabela LR, com linhas indexadas por estados e colunas indexadas por símbolos terminais e não-terminais da gramática.

#### Ações

- desloca s (shift s):
lê o próximo símbolo de entrada e empilha o estado s.

- reduz usando ```A → β```  (reduce)
retira n estados da pilha, onde ```n = | β |`` e executa ação (ei, A) da tabela LR (sempre um goto -- veja abaixo), onde ei é o estado que aparece no topo após a retirada dos n estados.

- desvia para s (goto s):
ação executada imediatamente após uma redução; 
corresponde a deslocar s para a pilha, sem leitura de símbolo de entrada, 
mas sim consultando o não-terminal obtido via redução.

- aceita (accept):
ação que indica reconhecimento da cadeia de entrada e provoca a parada do analisador.

- erro (error):
entradas em branco na tabela LR representam situações de erro sintático na entrada.

