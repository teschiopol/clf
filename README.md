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

### Cap 2.2 Automi a Pila

Sono potenti automi che hanno a disposizione una pilla pushdown per contenere quantità non limitata di dati. Tra deterministici e non deterministici c'è differenza computazionale.

Automi a pila non deterministici sono computazionalmente equivalenti alle grammatiche context-free.

Una sestupla (Q, $\sum$, $\Gamma$, $\delta$, q<sub>0</sub>, F) dove:

- Q è insieme degli stati
- $\sum$ è alfabeto dell'input
- $\delta$ è funzione transizione Qx$\sum$<sub>$\epsilon$</sub> x$\Gamma$<sub>$\epsilon$</sub>  -> P(Qx$\Gamma$<sub>$\epsilon$</sub> )
- S è stato iniziale
- q<sub>0</sub> è stato iniziale
- F è insieme degli stati accettanti

Nel diagramma di stato si scrive a,b -> c che vuol dire

- legge input a
- toglie b dalla cima della pila
- scrive c sulla pila

Se a è vuoto, può leggere e scrivere sulla pila senza input
Se b è vuoto, può scrivere senza togliere dalla pila
Se c è vuoto, può togliere dalla pila senza scrivere
