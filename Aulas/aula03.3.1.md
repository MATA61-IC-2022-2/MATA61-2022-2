# 3.3 Análise Sintática Ascendente

## 3.3.1 Análise LR(0)

#### Definição 1

Um item (ou item LR(0)) é uma produção na qual foi marcada uma posição do lado direito com o símbolo ```•```.

- Gramática:	

```
G = ({E},{a,b,+,*}, P, E)
P:  E → a | b | +EE | *EE
```
- Conjunto de todos os ítens de G:

```
I(G) = { E → •a , E → •b, E → •+EE,  E → •*EE, 
	 E → a• , E → b•, E → +•EE,  E → *•EE,
	 E → +E•E,  E → *E•E, E → +EE•,  E → *EE• }
``` 

Os ítens são usados para a construção de estados.

- Interpretação

A presença de um estado no topo da pilha que contém um item da forma ```A → α•β```  indica que já foi processada e deslocada para a pilha a parte ```α``` do redutendo ```αβ```.

- Item completo 

A presença de um estado no topo da pilha que contém um item da forma ```A → α•```  (item completo) indica que já  foi processado um redutendo completo.

Seja um estado no topo da pilha contendo um item incompleto da forma 

```  A → α•Bβ   com A,B ∈ VN e α,β ∈ (VN ∪ VT)* ```

O algoritmo de análise deverá aceitar qualquer cadeia derivável de B, ou seja:

O estado deverá conter ítens da forma ```B → •δ```.

#### Definição 2

Um conjunto K de ítens é _fechado_ se, 
para todo item de K da forma ```A → α•Bβ```, todos os ítens da forma ```B → •δ``` estão em K.  

**Fecho(K)** será o menor conjunto fechado que contiver K.

```
Ex. 1: 	
K1 = { E → +•EE }
Fecho(K1) = { E → +•EE, E → •a , E → •b, E → •+EE,  E → •*EE }
```
```
Ex.2:		
K2 = { E → +E•E, E → *•EE, E → •a}
Fecho(K2) = { E → +E•E, E → *•EE , E → •a, E → •b, E → •+EE,  E → •*EE }
```
```
Ex. 3:	
K3 = { E → •b }
Fecho(K3) = { E → •b }
```

#### Definição 3

Um estado é um conjunto fechado de ítens.

#### Definição 4

Se um estado ei contém um item incompleto da forma 

```A → α•Xβ,  X ∈ (VN ∪ VT)```,  
ei está no topo da pilha e o próximo símbolo consultado for X, 
então a parte ```αX`` do redutendo terá sido processada, devendo ser empilhado um estado ej 
que contenha o item ```A → αX•β```.


#### Definição 5

A função **goto(K,X)** é o fecho  do conjunto de todos os ítens 
da forma ```A → αX•β```, tais que o item ```A → α•Xβ``` está em K.

```
Ex. 4:
K1 = { E → *•EE }
goto(K1,E) = { E → *E•E, E → •a , E → •b, E → •+EE,  E → •*EE }

goto(K1,*) = ∅
``` 

### Construção de Estados LR(0)

#### Convenções

- Usar a gramática aumentada G’, acrescentando às produções de G 
a produção ```S’ → S$```, onde ```$ ∉ T```, S é o símbolo inicial de G e S’ é o símbolo inicial de G’.

- O símbolo $ está no final de toda e qualquer cadeia de entrada.

- Estado inicial e0

O estado inicial contém o item ```S’ → •S$```.
A construção de estados LR(0) partirá do estado inicial e0, 
obtendo novos estados a partir da aplicação de fecho(K) e goto(K,X), 
até que não se obtenham mais novos estados.


### Algoritmo para determinar os estados LR(0) de uma gramática

Seja  C um conjunto de estados.

- Adota-se o estado ```e0  = fecho({S’ → •S$})```  como valor inicial do conjunto C.

- Se existe um estado ei de C e um símbolo ```X ∈ (N ∪ T)``` tais que 
o conjunto ej = goto(e,X) não é vazio e ej ainda não está em C, 
então acrescente ej ao conjunto C.

- O passo é repetido até que não se possam acrescentar mais estados ao conjunto C.

- C é o conjunto de estados LR(0) de G.

#### Exemplo

```
Ex. 5:

E’ → E$   
E →  +EE 
E →  *EE
E → a 
E → b
```

```
e0  =  fecho({E’ → •E$})
E’ → •E#
E → •+EE  	E → •*EE  	E → •a  	E → •b

e1  =  goto(e0,E)
E’ → E•#  (aceitação)

e2  =  goto(e0,+)
E → +•EE
E → •+EE  	E → •*EE 	E → •a    		E → •b

e3  =  goto(e0,*)
E → *•EE
E → •+EE  	E → •*EE 	E → •a    		E → •b

e4  =  goto(e0,a)
E → a• 

e5  =  goto(e0,b)
E → b•

e6  =  goto(e2,E)
E → +E•E
E → •+EE  	E → •*EE 	E → •a    		E → •b

e2  =  goto(e2,+) 	e3  =  goto(e2,*) 	e4  =  goto(e2,a) 	e5  =  goto(e2,b)

e7  =  goto(e3,E)
E → *E•E
E → •+EE  	E → •*EE 	E → •a    		E → •b

e2  =  goto(e3,+) 	e3  =  goto(e3,*) 	e4  =  goto(e3,a) 	e5  =  goto(e3,b)

e8  =  goto(e6,E)
E → +EE•  

e9  =  goto(e7,E)
E → *EE•
```

#### Definição 6

Uma gramática é do tipo LR(0) se seus estados contêm apenas ítens completos ou apenas ítens incompletos.
Nesse caso, as reduções podem ser realizadas sem consultar o próximo símbolo na entrada.

##### Tabela LR(0)

|  | + | * | a | b | $ | E | 
|--|---|---|---|---|---|---|
|e0|e2 |e3|e4|e5| |e1|
|e1|   |  |  |  |__a__| |
|e2|e2 | e3 | e4 | e5 | | e6 |
|e3|e2 | e3 | e4 | e5 | | e7 |
|e4|r3 | r3 | r3 | r3 | r3 | |
|e5|r4 | r4 | r4 | r4 | r4 | |
|e6|e2 |e3 |e4 |e5 | |e8 |
|e7|e2 |e3 |e4 |e5 | |e9 |
|e8|r1 |r1 |r1 |r1 |r1 | |
|e9|r2 |r2 |r2 |r2 |r2 | |

##### Ações

- ei: empilha o estado i

- rj: reduz usando a regra j

- a: aceita a cadeia de entrada

- em branco: rejeita a cadeia de entrada (erro sintático)

##### Análise da cadeia *a+ba

|Passo|Pilha|VN|Cadeia|Ação|
|-----|-----|-----|------|----|
| 0   |e0          |   | ```*a+ba$```|e3 |
| 1   |e0 e3       |   | ```a+ba$``` |e4 |
| 2   |e0 e3 e4    |   | ```+ba$```  |r3 |
| 3   |e0 e3       | E | ```+ba$```  |e7 |
| 4   |e0 e3 e7    |   | ```+ba$```  |e2 |
| 5   |e0 e3 e7 e2 |   | ```ba$```   |e5 |
| 6   |e0 e3 e7 e2 e5 |   | ```a$``` |r4 |
| 7   |e0 e3 e7 e2 | E | ```a$```    |e6 |
| 8   |e0 e3 e7 e2 e6 |   | ```a$``` |e4 |
| 9   |e0 e3 e7 e2 e6 e4 |   | ```$``` |r3 |
| 10  |e0 e3 e7 e2 e6 | E | ```$```  |e8 |
| 11  |e0 e3 e7 e2 e6 e8 |   | ```$``` |r1 |
| 12  |e0 e3 e7    | E | ```$```     |e9 |
| 13  |e0 e3 e7 e9 |   | ```$```     |r2 |
| 14  |e0          | E | ```$```     |e1 | 
| 15  |e0 e1       |   | ```$```     |__a__ |

#### Outro Exemplo

```Ex.6

G1 = ({E,T,F}, {a,b,+,*,(,)}, P1, E)

P1:
E’ → E#
E → E  + T | T			
T → T  *  F | F
F → (E ) | a
```

G1 não é LR(0).

```
e0  =  fecho({E’ → •E#})
E’ → •E #
	...

e2 = goto(e0,T)

     E → T•
     T → T• * F

	...

e9 = goto(e6,T)

     E → E + T•
     T → T• * F
	...
```

#### Definição 7

Uma gramática é do tipo LR(1) se a decisão quanto à realização de um deslocamento ou de uma redução 
puder se basear apenas no próximo símbolo de entrada.

#### Definição 8

Follow(X) o conjunto de símbolos terminais que podem seguir o símbolo X em uma forma sentencial.

#### Algoritmo para calcular Follow(X),  X ∈ VN 

- ```$``` está em Follow(S).

- Se existe uma produção ```A → αΒβ, β ≠ ε``, então Follow(B) contém ```First(β)```.

- Se existe uma produção ```A → αΒ``` ou ```A → αΒβ``` e ```nullable(β)``` , então Follow(B) contém Follow(A).

#### Definição 9

Uma gramática é do tipo SLR -- Simple LR -- se a decisão quanto à realização de um deslocamento ou de uma redução puder se basear no próximo símbolo de entrada e no conjunto Follow(X).

Se ```[A → α•]``` está em ei, então faça a ação action[i,a] igual a "reduzir usando ```A → α```" para todo _a_ que aparece em FOLLOW(A) (exceto para S’).


