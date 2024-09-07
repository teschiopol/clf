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

#### Forma normale di Chomsky

Se ogni regola della grammatica è della forma:

- A -> BC
- A -> a

Per ottenerla:

- Aggiungiamo nuova variabile iniziale
- Eliminiamo le regola A -> $\epsilon$, poi in ogni regola dove appare A nel lato destro, scriviamo tutte le occorenze senza la A.
  - A -> $\epsilon$ fa diventare S -> ASA | aB in S -> ASA | aB | SA | AS | S
- Eliminiamo le regole unitarie A -> B, poi aggiungiamo A -> u per la regola B -> u, dove u è una stringa di variabili e terminali
- Rimpiazziamo le regole A->u<sub>1</sub>u<sub>2</sub>u<sub>3</sub> in poi con A->u<sub>1</sub>A<sub>1</sub> e A<sub>1</sub>->u<sub>2</sub>A<sub>2</sub> e A<sub>2</sub> -> u<sub>3</sub>.
- Infine convertimo le u<sub>i</sub> che sono terminali con una nuova regola U<sub>i</sub> -> u<sub>i</sub> e sostituiamo i terminali.
