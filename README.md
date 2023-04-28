<!-- omit in toc -->
# Progetto d'esame per l'a.a. 2022/2023

- [Introduzione](#introduzione)
- [Preparazione](#preparazione)
- [Relazione](#relazione)
- [Consegna](#consegna)
  - [Come creare l'archivio](#come-creare-larchivio)
- [Valutazione](#valutazione)

## Introduzione

Questa repository contiene la descrizione dei temi proposti per il progetto
d'esame per l'a.a. 2022/2023 e le modalità per la preparazione e la consegna.

Il progetto d'esame consiste nell'implementazione di uno o più programmi in C++,
accompagnati da una breve relazione di presentazione.

I progetti proposti riguardano:

- [Simulazione dell'evoluzione di una pandemia](epidemia.md)
- [Simulazione del comportamento di stormi](boids.md)
- [Dinamica in un biliardo triangolare](biliardo.md)

E' possibile presentare il progetto su un altro tema a propria scelta, purché di
complessità paragonabile e concordato preventivamente con i docenti.

## Preparazione

Raccomandiamo di svolgere il progetto in gruppo, fino a un massimo (non
derogabile) di quattro persone. Il progetto può però essere preparato anche
singolarmente.

Il programma deve essere scritto in C++ standard, seguendo le indicazioni e le
raccomandazioni fornite a lezione nel corso dell'anno. E' ammesso l'uso di
librerie esterne (ad esempio per la grafica), ma queste devono essere
disponibili sulla piattaforma di riferimento (Ubuntu 22.04, con il compilatore
gcc v. 11.3).

Ogni programma deve essere costituito da **almeno due** *translation unit*.
Indicativamente la logica del programma va suddivisa tra uno o più header file
(`.hpp`) e tra uno o più file sorgente (`.cpp`); la funzionalità va poi
richiamata da un ulteriore file contenente il `main`.

La compilazione e l'esecuzione non devono generare messaggi diagnostici
compilando il codice con le opzioni `-Wall -Wextra
-fsanitize=address,undefined`. Nel caso dovessero esserci segnalazioni generate
da codice di terzi (ad es. dalla libreria grafica), indicarle nella relazione.

Il codice deve essere formattato adeguatamente (con `clang-format` o tool
equivalente). Il file di configurazione del tool di formattazione (ad es.
`.clang-format`) deve essere consegnato insieme al progetto.

Nomi di file, funzioni, tipi, variabili, ecc. devono essere descrittivi e
seguire convenzioni ortografiche e di lingua uniformi.

I nomi di file e directory non devono contenere spazi ed è preferibile che siano
in carattere minuscolo.

E' richiesta la scrittura di unit test, usando *Doctest* o altro strumento
analogo.

Pur non essendo necessari, saranno valutati positivamente l'uso di *CMake* per
la compilazione, l'uso di *Git* come strumento collaborativo e l'adozione di
ogni altro strumento utile al miglioramento del software prodotto.

Se lo sviluppo avviene in una repository *Git*, potete indicarne l'indirizzo
nella relazione; se la repository è privata ed è tenuta su
[GitHub](https://github.com/), potete condividerla con noi aggiungendo gli
account `giacomini`, `battibass`, `fferrari1990`, `rsreds`, `JustWhit3` e
`GColom` tra i membri del progetto. Naturalmente questo **non** sostituisce la
consegna secondo le modalità indicate sotto.

## Relazione

La relazione di accompagnamento rappresenta una guida alla comprensione del
codice e alla valutazione del lavoro nel suo complesso. Indicativamente deve
contenere:

- autore o autori del lavoro
- descrizione sintetica delle principali scelte progettuali e implementative
- istruzioni su come compilare, testare, eseguire
- descrizione del formato di input e di output, possibilmente con degli esempi
- interpretazione dei risultati ottenuti
- strategia di test per verificare che quanto ottenuto sia ragionevolmente
  esente da errori
- ogni altra informazione utile agli obiettivi sopra citati

La relazione deve essere in formato `pdf` o *markdown* (il formato con cui è
composto questo testo). Per un risultato tipografico eccellente si suggerisce di
provare LaTeX, o sul proprio PC o su strumenti online, ad es.
[overleaf](https://overleaf.com). Se si usano altri sistemi (ad es. MS Word o
LibreOffice), ricordarsi di esportare in formato `pdf`.

## Consegna

La consegna avverrà su virtuale.unibo.it in prossimità di ogni appello
(indicativamente 10 giorni prima) tramite un file archivio `.zip` o `.tgz`. Ogni
studente/studentessa deve inviare l'archivio, anche se il lavoro è svolto in
gruppo. La consegna va fatta ogni volta che ci si iscrive per un appello, anche
se nel frattempo non sono intercorse modifiche al codice. Se il lavoro è svolto
in gruppo ed è lo stesso per tutti i componenti del gruppo, chiediamo di
caricare lo stesso identico archivio.

L'archivio deve contenere:

- il codice sorgente e tutte e sole le risorse necessarie alla compilazione e
  all'esecuzione (ad esempio il file `CMakeLists.txt` ed eventuali immagini e
  font)
- una breve relazione di accompagnamento

L'archivio **non** deve contenere altro. Ad titolo puramente indicativo,
l'archivio non deve contenere:

- eseguibili/binari ottenuti compilando il sorgente
- directory quali `__MACOSX` o simili

Prima di creare l'archivio, verificate il contenuto e fate pulizia di tutto
quanto non va consegnato.

### Come creare l'archivio

Supponendo che tutto il codice e la relazione si trovino in una cartella
`progetto`, per creare un archivio `zip`:

```shell
$ ls
progetto
$ zip -r progetto.zip progetto
$ ls
progetto progetto.zip
```

Per creare un archivio `tgz`:

```shell
$ ls
progetto
$ tar zcf progetto.tgz progetto
$ ls
progetto progetto.tgz
```

Prima di produrre l'archivio sincerarsi che la directory contenga la relazione.
Una volta creato l'archivio, consigliamo di sincerarsi che, una volta
scompattato, contenga tutto quanto necessario per la compilazione e
l'esecuzione.

## Valutazione

La valutazione si basa su cinque criteri:

- La **qualità della relazione** intende valutare la capacità della relazione di
  accompagnare il lettore nella comprensione del programma, nelle varie scelte
  di design, di implementazione, di ricerca della correttezza. Si tiene inoltre
  in conto la correttezza lessicale e grammaticale, nonché l'uso corretto della
  lingua italiana.

- La **qualità del design** del programma intende valutare quanto il design
  dell'applicazione è appropriato per risolvere il problema proposto. Elementi
  considerati sono, a titolo esemplificativo, la suddivisione del codice in
  classi e funzioni dai nomi significativi, la loro progettazione e il loro uso
  secondo le indicazioni date a lezione, la *const-correctness*, la suddivisione
  del codice in più file sorgente, il riuso di componenti terzi, in particolare
  della standard library.

- La **qualità dell'implementazione** del programma intende valutare
  l'applicazione corretta ed efficiente dei costrutti del linguaggio C++
  nell'implementazione del programma secondo le convenzioni consolidate e
  proposte a lezione. Verrà anche considerata, ad esempio, la corretta
  formattazione del codice.

- La **correttezza del programma** intende valutare quanto il comportamento del
  programma in esecuzione sia aderente a quanto specificato nella consegna e,
  per quel che riguarda aspetti non specificati o eventuali varianti, nella
  relazione. Verranno anche considerate le strategie e le tecniche utilizzate
  per verificare che il programma si comporti correttamente.

- L'**originalità della soluzione** intende valutare innanzitutto il rispetto di
  quanto previsto nella descrizione del progetto, almeno nella opzione di base.
  Un giudizio oltre la sufficienza dipende dall'esplorazione di altre opzioni e
  varianti ovvero dall'utilizzo di strumenti, librerie, tecniche aggiuntivi.

Ogni criterio sarà valutato secondo la scala: *insufficiente*, *sufficiente*,
*buono*, *ottimo*. Indipendentemente dalla valutazione complessiva ottenuta, la
sufficienza si intende acquisita solo se la valutazione di ogni singolo criterio
è almeno sufficiente.

La valutazione del progetto vale per tutto l'anno accademico, ma è possibile
fare ulteriori consegne per eventualmente migliorare la propria valutazione,
anche se il lavoro era stato fatto originariamente in gruppo; in tal caso vanno
indicate nella relazione le variazioni intercorse rispetto alla consegna
precedente.
