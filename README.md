# CLF

# Cap 2 - Linguaggi Context-Free

## Cap 2.1 Grammatiche Context-Free

Una quadrupla (V, $\sum$, R, S) dove:
- V è insieme delle variabili
- $\sum$ è insieme terminali
- R è insieme delle regole
- S è stato iniziale

### Progettare grammatiche context-free

Prima si costruisce il DFA per il linguaggio regolare, poi lo si trasforma in CFG.

- Una variabile R per ogni stato
- Regola R~i~ -> aR~q~ se c'è transazione da stato i a stato q tramite a nel DFA
- Regola  R~i~ -> $\epsilon$ se stato i è accettante
