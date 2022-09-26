# MATA61 - Compiladores

>### _A good programming language is a conceptual universe for thinking about programming._
>— Alan Perlis

  * [Calendário Acadêmico](https://supac.ufba.br/sites/supac.ufba.br/files/calendario_academico_2022-1-2_ufba_-_aprovado_07.10.21_-_atualizado_04.03.22.pdf)
  * [Ementa](#ementa)
  * [Programa](#programa)
  * [Métodos](#m-todos)
  * [Avaliação](#avalia--o)
  * [Plano de Aulas](#plano-de-aulas)
  * [Material de Apoio](#material-de-apoio)
  * [Bibliografia](#bibliografia)

(<small><i>Table of contents generated with <a href='http://ecotrust-canada.github.io/markdown-toc/'>markdown-toc</a></i></small>)

## Ementa

Análise e Síntese. Análise léxica, sintática e semântica. Geração de código intermediário. Otimização de código
intermediário. Geração e otimização de código objeto.

## Programa

1. Introdução à Compilação de Programas:
   a) Conceitos básicos e funcionalidades;
   b) Componentes de um compilador;
   c) Fases de Análise e Síntese. 
2. Análise Léxica: 
  a) Conceitos básicos (tokens, lexemas, etc.);
  b) Especificação e reconhecimento de linguagens regulares;
  c) Implementação e geração de analisadores léxicos.
3. Análise Sintática: 
  a) Conceitos básicos (derivação, árvores sintáticas, ambiguidade, etc.);
  b) Especificação e reconhecimento de linguagens livres de contexto; 
  c) Análise LL e LR;
  d) Implementação e geração de analisadores sintáticos;
  e) Árvores sintáticas abstratas.
4. Análise semântica: 
  a) Conceitos básicos;
  b) Sistemas de tipos;
  c) Tabela de símbolos e resolução de nomes;
  d) Implementação de verificação de tipos. 
5. Representação intermediária 
6. Ambientes de execução, organização de memória
  a) Heap Management
  b) Stack Management
7. Geração de código 
8. Otimização de código

## Métodos

- Aulas presenciais
- Leituras e discussões
- Quizzes e exercícios para explorar conceitos de compiladores e sua implementação
- Trabalho prático de construção de um compilador.

### Plataformas de Apoio

- Google Classroom
- GitHub
 
## Atividades 
 
- Trabalho Prático:  Projetar e implementar um compilador (incluindo Analisador Léxico, Analisador Sintático, Analisador Semântico e Gerador de Código) para uma linguagem simples e de alto nível.
- Outras Atividades: Quizzes,  exercícios individuais

## Avaliação

+ Conceitos de compiladores (25%)
   - Quizzes
   - Exercícios
+ Prova (20%)
+ Implementação de um compilador (55%)

## Plano de Aulas

Data | Semana | Tópico
-- | -- | --
15 e 17/08/2022 | 1 | Apresentação da disciplina; Conceitos básicos de compiladores
22 e 24/08/2022 | 2 | Análise léxica, revisão de expressões regulares, autômatos finitos; Implementação e geração de analisadores léxicos
29 e 31/08/2022 | 3 | Flex; Especificação do trabalho prático 1; Conceitos básicos de análise sintática
05 e 07/09/2022 | 4 | Conceitos básicos de análise sintática; FERIADO
12 e 14/09/2022 | 5 | Análise sintática descendente; Análise preditiva
19 e 21/09/2022 | 6 | Análise LL(1)
26 e 28/09/2022 | 7 | Análise sintática ascendente; Análise SLR
03 e 05/10/2022 | 8 | Análise LR(1); Análise LALR; Bison (Aulas remotas - CBSOFT / SBES 2022)
10 e 12/10/2022 | 9 | Integração entre Bison e Flex; FERIADO
17 e 19/10/2022 | 10 | Exercícios; Especificação do trabalho prático 2 (Aula remota - Palestra no ERES 2022)
24 e 26/10/2022 | 11 | Análise Semântica
31/10 e 02/11/2022 | 12 |  
07 e 09/11/2022 | 13 |  
14 e 16/11/2022 | 14 | 
21 e 23/11/2022 | 15 | 
05 e 07/12/2022 | 16 | 
12 e 14/12/2022 | 17 | 

## Material de Apoio

- Algumas [aulas em markdown](./Aulas/README.md)
- [Especificação da linguagem C-](./CMinus/README.md)
- Especificação e implementação do compilador: Repositórios na organização mata61-ic-ufba-2022-2.org no GitHub.
- Exercícios práticos de implementação, textos em formato markdown: Repositórios na organização mata61-ic-ufba-2022-2.org no GitHub. 
- Exercícios, quizzes, textos em formato .PDF, slides e vídeos: Google Classroom da UFBA, disciplina MATA61 2022.2 T01.
- Tutoriais: Git & GitHub Basics; Git-it: https://github.com/jlord/git-it-electron/releases

## Bibliografia

### Básica

1. THAIN, Douglas. Introduction to Compilers and Language Design. 2a Ed, 2020, http://compilerbook.org.
2. AHO, A. et al. Compiladores: princípios, técnicas e ferramentas. 2a Ed., Addison-Wesley, 2008. 

### Complementar

1. LEVINE, John. Lex & Bison. O'Reilley. 2009.
2. APPEL, A. W. Modern Compiler Implementation in Java. Cambridge University Press, Cambridge, 1997. 
3. LOUDEN, K. C. Compiladores: Princípios e Práticas. Editora Thompson Pioneira, 1a Ed., 2004. 
4. RICARTE, I. Introdução à Compilação, Editora Campus, 2008. 
5. BROWN, D.; LEVINE, J. ; MASSON, T. Lex & Yacc. Unix Programming Tool. O'Reilly, 2nd edition, 1995. 
6. MITCHELL, J. Foundation for Programming Languages. Foundations of Computing, MIT Press, 1996. 
7. WINSKEL, G. The Formal Semantics of Programming Languages: An Introduction. Foundations of Computing series. MIT Press, Cambridge, Massachusetts, February 1993. 
8. SCOTT, M.L. Programming Language Pragmatics, 3rd ed.
9. ABELSON, H.; SUSSMAN, G.; with SUSSMAN, J. A book for your shelf: [Structure and Interpretation of Computer Programs](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html),  2nd ed.

----
  Distributed under the MIT License. See [LICENSE](LICENSE) for more information.
  This is an organization for academic activities. See [Authors](AUTHORS).
