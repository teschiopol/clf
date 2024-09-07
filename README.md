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

#### Equivalenza con le grammatiche context-free

Un linguaggio è context-free se e solo se esiste un automa a pila che lo riconosce.

Se un linguaggio è context-free, allora esiste un automa a pila che lo riconosce.

```Convertiamo da una CFG G a un PDA P```

Dobbiamo realizzare una pila che dato un input, riuscirà a generarlo. Alla fine li confronteremo e accetteremo se uguali.
Per farlo lavoreremo sulle stringhe intermedie generate ad ogni derivazione. Quindi distinguiamo il comportamento in base a se troviamo una variabile o un terminale sulla cima della pila.

1) Inserisce simbolo marcato $ e la prima variabile nella pila
2) Se sulla cima della pila c'è A, scegli non deterministicamente una regola per A e sostituisce con la parte destra di A
3) Se sulla cima della pila c'è terminale a, legge l'input e lo confronta. Se sono uguali, ripete. Se sono diversi, rifiuta su questo ramo
4) Se sulla cima c'è il simbolo $, entra nello stato accettante. L'input è stato completamente letto
5) Ripete dal punto 2

Nuova notazione (r, u) $\in$ $\delta$(q, a, s)
Siamo nello stato q, leggiamo a dal input, s è nella cima della pila. Andremo allo stato r e nella pila sostituiremo s con u.

Nel diagramma del PDA avremo stato q<sub>start</sub> con inserimento di \$.
Lettura variabile iniziale.
Stato q<sub>loop</sub> con le regole per i terminali e sostituzione parte destra per le variabili.
Stato q<sub>accept</sub> quando leggo il $ dalla pila e sono quindi vuoto.
___

Se un linguaggio è riconosciuto da un automa a pila, allora è context-free.

```Convertiamo da PDA a CFG```
