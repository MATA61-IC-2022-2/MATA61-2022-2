# 3.3 Análise Sintática Ascendente

## 3.3.2 Análise LR(1)

O autômato LR(0) é limitado porque ele não analisa quais são os tokens
que podem "seguir" de fato uma regra de produção.
A análise SLR contorna tal limitação por meio dos conjuntos 
FOLLOW, usados para decidir quando fazer a redução.

A forma completa ou “canônica” da análise LR(1) depende de autômatos LR(1).
O autômato LR(1) parece com o LR(0), mas estende cada item com anotações sobre
o conjunto de tokens que podem seguí-lo, dado o estado corrente da análise.
Tal conjunto é conhecido com o _lookahead_ do item.
O conjunto _lookahead_ é sempre um subconjunto de FOLLOW do não-terminal relevante.




