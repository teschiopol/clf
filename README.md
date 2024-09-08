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
- $\Gamma$ è alfabeto della pila
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

G dovrebbe generare una stringa, se quella stringa fa andare P da uno stato iniziale ad accettante.

Ideare una variabile A<sub>pq</sub> che porta la pila da p a q, nello stesso stato.

Il PDA sarà

- unico stato accettante
- svuota la pila prima di accettare
- una transizione o push o pop

___

Ogni linguaggio regolare è context-free.
Questo perché un linguaggio regolare è riconosciuto da un automa finito. Quest'ultimo è un automa a pila che ignora la sua pila.

### Cap 2.3 Linguaggi non Context-Free

#### Pumping Lemma

Se A è linguaggio context-free, allora esiste un numero p tale che, se s è una stringa in A di lunghezza almeno p, può essere divisa in cinque parti s = uvxyz:

1) per ogni i >= 0, uv<sup>i</sup>xy<sup>i</sup>z $\in$ A
2) |vy| > 0
3) |vxy| <= p

Alcuni linguaggi non context-free:

- a<sup>n</sup>b<sup>n</sup>c<sup>n</sup>  | n >= 0 -> pumping up
- a<sup>i</sup>b<sup>j</sup>c<sup>k</sup> | 0 <= i <= j <= k -> pumping up e pumping down
- ww | w $\in$ {0, 1}<sup>*</sup> -> usando 0<sup>p</sup>1<sup>p</sup>0<sup>p</sup>1<sup>p</sup>

## Cap 3 - La tesi di Church-Turing

### Cap 3.1 Macchine di Turing

Simile ad un automa, memoria illimitata.

- Può sia scrivere sia leggere sul nastro
- La testina si muove a destra e sinistra
- Nastro è infinito
- Gli stati di accettazione e rifiuto sono immediati

#### Definizione formale di macchina di Turing

Una setupla (Q, $\sum$, $\Gamma$, $\delta$, q<sub>0</sub>, q<sub>accept</sub>, q<sub>reject</sub>) dove:

- Q è insieme degli stati
- $\sum$ è alfabeto dell'input senza simbolo blank
- $\delta$ è funzione transizione Qx$\Gamma$ -> P(Qx$\Gamma$x{L, R} )
- $\Gamma$ è alfabeto del nastro con blank
- q<sub>0</sub> è stato iniziale
- q<sub>accept</sub> è stato di accettazione
- q<sub>reject</sub> è stato di rifiuto

La configurazione è lo stato della macchina durante la computazione, composto dalla posizione della testina e della situazione del nastro.

La configurazione C<sub>1</sub> produce la configurazione C<sub>2</sub> se la MdT passa tra le due in un unico passo.

Un linguaggio è <strong>Turing-riconoscibile</strong> se esiste una MdT che lo riconosce.

L'insieme delle stringhe che M accetta rappresenta il linguaggio riconosciuto da M.

Una stringa è accettata se produce una serie di configurazioni che terminano in uno stato di accettazione.

Le MdT che si fermano su ogni input sono dette decisori, in quanto decidono se accettare o rifiutare, non ciclano mai. Un decisore decide un linguaggio se riconosce tale linguaggio.

Un linguaggio è <strong>Turing-decidibile</strong> se esiste una MdT che lo decide.

Ogni linguaggio decidibile è Turing-riconoscibile.

#### Esempi di macchine di Turing

Descrizione di come si muove la testina, dei controlli che fa sullo stato che è ed eventuali sostituzioni.

### Cap 3.2 Varianti di macchine di Turing

Sono delle varianti che non vanno però a modificare la classe di linguaggi riconosciuti o aumentare il potere computazionale.

#### Macchina di Turing multinastro

Inizialmente solo nastro 1 ha input, gli altri vuoti. Ogni testina è su un nastro.

Ogni macchina multinastro ha una MdT a nastro singolo equivalente.

Lo si fa usando il simbolo # per delimitare l'inizio e la fine dei nastri, inoltre si aggiunge il simbolo puntato per identificare la testina virtuale dei vari nastri.

#### Macchina di Turing non deterministica
