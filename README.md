# CLF

## Cap 2 - Linguaggi Context-Free

### Cap 2.1 Grammatiche Context-Free

Una quadrupla (V, $\sum$, R, S) dove:

- V è insieme delle variabili
- $\sum$ è insieme terminali
- R è insieme delle regole
- S è stato iniziale

#### Progettare grammatiche context-free

Prima si costruisce il DFA per il linguaggio regolare, poi lo si trasforma in CFG.

- Una variabile R per ogni stato
- Regola R<sub>i</sub> -> aR<sub>q</sub> se c'è transazione da stato i a stato q tramite a nel DFA
- Regola  R<sub>i</sub> -> $\epsilon$ se stato i è accettante

Grammatiche possono generare stessa stringa in modi diversi, sono dette ambigue. Se linguaggi possono essere generati solo così, sono detti inerentemente ambigui. Es: a<sup>i</sup>b<sup>j</sup>c<sup>k</sup> | i = j oppure j = k

#### Formula normale di Chomsky

Ogni regola è della forma

- A -> BC
- A -> a
