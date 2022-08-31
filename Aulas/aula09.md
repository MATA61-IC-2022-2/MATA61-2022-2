# Ambientes de Tempo de Execução

- Objetivo: Estudar algumas técnicas padrão para estruturar código executável que são amplamente utilizadas.

- Agenda
   + Gerenciamento de recursos em tempo de execução
   + Correspondência entre estruturas estáticas e dinâmicas
   + Organização de memória

## Gerenciamento de recursos em tempo de execução (runtime)

### Recursos em tempo de execução 
   
+ A execução de um programa está inicialmente sob o controle do sistema operacional (SO)
+ Quando um programa é invocado:
   - O SO aloca espaço para o programa
   - O código é carregado em parte do espaço
   - O SO desvia para o ponto de entrada (ou seja, "main").

### Laioute de memória
<img src="https://github.com/MATA61-IC-2022-2/MATA61-2022-2/blob/8f7d5adbf703476ac065a7861dc298a40213136d/Aulas/figuras/Screen%20Shot%202022-08-30%20at%2020.18.01.png" width="350" height="250">

Tradicionalmente, as imagens da organização da máquina possuem:
- Endereço baixo no topo
- Endereço alto na parte inferior
- Linhas delimitando áreas para diferentes tipos de dados

Tais imagens são simplificações:
- Por exemplo, nem toda memória precisa ser contígua

### O que é "Other Space"?

- Contém todos os dados para o programa
   + "Other Space" = "Data Space"
- O compilador é responsável por:
   + Geração de código
   + Orquestração do uso da área de dados

### Objetivos da geração de código

### Premissas sobre execução

### Ativações

### Tempo de vida de variáveis

### Árvores de ativação

### Laioute de memória revisado

### Registros de ativação

### Laioute de memória com dados estáticos

## Gerenciamento da "Heap"

### Armazenamento na "Heap"

###  Laioute de memória com a "Heap" 

<img src="https://github.com/MATA61-IC-2022-2/MATA61-2022-2/blob/f22c3174ad2daaeb7191d5bceaae3c1d6f7d5d73/Aulas/figuras/Screen%20Shot%202022-08-30%20at%2020.54.14.png" width="350" height="250">

## Stack Machines

+ Um modelo de avaliação simples:
   - Sem variáveis ou registros
   - Uma pilha de valores para resultados intermediários
+ Cada instrução:
   - Pega seus operandos do topo da pilha
   - Remove esses operandos da pilha 
   - Executa a operação necessária com eles 
   - Coloca o resultado na pilha
