<!-- omit in toc -->
# Simulazione di stormi

- [Descrizione del problema](#descrizione-del-problema)
- [Controllo dei vicini](#controllo-dei-vicini)
- [Le regole di volo](#le-regole-di-volo)
  - [Regola 1: separazione](#regola-1-separazione)
  - [Regola 2: allineamento](#regola-2-allineamento)
  - [Regola 3: coesione](#regola-3-coesione)
- [Implementazione del modello](#implementazione-del-modello)
- [Comportamento ai bordi](#comportamento-ai-bordi)
- [Variazioni sul tema](#variazioni-sul-tema)
- [Suggerimenti sull'implementazione](#suggerimenti-sullimplementazione)
- [Riferimenti utili](#riferimenti-utili)

## Descrizione del problema

Il progetto consiste nell'implementazione di una simulazione del comportamento
degli stormi di uccelli in volo in uno spazio bidimensionale.

Reso noto da un software di intelligenza artificiale realizzato nel 1986, la
simulazione si basa sull'interazione tra agenti detti *boids* in uno spazio. Nel
modello più elementare gli agenti determinano la loro traiettoria tramite tre
regole:

- *separazione*: un boid si allontana dai boids vicini
- *allineamento*: un boid tende ad allinearsi alle traiettorie dei boids vicini
- *coesione*: un boid tende a muoversi verso il baricentro dei boids vicini

Modelli più complessi introducono altre regole, per esempio per evitare gli
ostacoli o per gestire stormi differenti.

## Controllo dei vicini

Le regole di volo vengono applicate tenendo conto dei boids "vicini". La
vicinanza tra boids può essere determinata in base alla loro posizione. Dato un
boid $b_i$, i suoi vicini sono tutti i boids $b_j$ per cui:

```math
\left| \vec{x}_{b_i}-\vec{x}_{b_j}\right| \lt {d}
```

## Le regole di volo

Le regole di volo vengono usate per determinare ognuna una componente della
variazione di velocità del boid a cui vengono applicate.

Per ogni boid $b_i$:

```math
\begin{align*} \vec{v}_{b_i} &= \vec{v}_{b_i} + \vec{v}_1 + \vec{v}_2 + \vec{v}_3 \\
\vec{x}_{b_i} &= \vec{x}_{b_i} + \vec{v}_{b_i} \Delta t \end{align*}
```

dove $\vec{v}_1$, $\vec{v}_2$ e $\vec{v}_3$ sono le velocità ottenute
dall'applicazione delle tre regole.

### Regola 1: separazione

La regola ha lo scopo di evitare che i boids collidano tra di loro.

```math
\vec{v}_1 = -s\sum_{j\ne i}(\vec{x}_{b_j}-\vec{x}_{b_i})\quad \text{se}\quad \left| \vec{x}_{b_i}-\vec{x}_{b_j}\right| \lt {d}_s$$
```

Usando la distanza come fattore per determinare la nuova velocità permette di
avere una accelerazione graduale del boid che si allontana. Un opportuno fattore
di separazione $s$ determina l'intensità della repulsione. La distanza $d_s < d$
stabilisce il range di influenza della regola.

### Regola 2: allineamento

Lo scopo della regola è fare in modo che i boids procedano nella stessa
direzione dello stormo.

```math
\vec{v}_2 = a(\frac{1}{n-1}\sum_{j\ne i}\vec{v}_{b_j} - \vec{v}_{b_i})$$
```

Viene sottratta alla media delle velocità dei boids (escluso il boid su cui è
applicata la regola) la velocità attuale del boid $b_i$. Il tutto moltiplicato
per un fattore di allineamento $a<1$ che determina la rapidità con cui il boid
sterza.

### Regola 3: coesione

La regola induce il boid a volare verso il centro di massa dei boid vicini. Il
centro di massa è dato da:

```math
\vec{x}_{c} = \frac{1}{n-1}\sum_{j\ne i}\vec{x}_{b_j}$$
```

La velocità $\vec{v}_3$ si ottiene sottraendo la posizione attuale del boid alla
posizione del centro di massa, moltiplicando poi il risultato per un fattore di
coesione $c$ opportuno:

```math
\vec{v}_3 = c(\vec{x}_{c}-\vec{x}_{b_i})$$
```

## Implementazione del modello

Progettare e implementare un programma che riproduca il modello sopra descritto.

Il programma accetta in input almeno il numero di boids e i parametri $d$, $d_s$, $s$, $a$ e $c$ delle regole di volo.

Il programma dovrebbe mostrare in output alcuni parametri di descrizione collettiva dello stormo, quali l'andamento nel tempo della distanza media tra i boids e della loro velocità media e le rispettive deviazioni standard.

Se propriamente simulati, i boids nel tempo dovrebbero tendere ad avvicinarsi e ad avere velocità mediamente simili tra di loro, assumendo il comportamento di uno stormo coeso.

## Comportamento ai bordi

Si suggerisce di implementare una regola per determinare il comportamento di un
boid quando raggiunge un bordo dell'area di simulazione. Due esempi di strategia
di implementazione posso essere:

- Lo spazio bidimensionale è toroidale, imponendo la periodicità dell'area di
simulazione: se un boid supera un bordo dell'area di simulazione, viene
"teletrasportato" al lato opposto.

- Si può introdurre una regola di volo che spinge un boid ad allontanarsi dai
  bordi: se un boid supera un bordo dell'area di simulazione, gli viene sommata
  una velocità diretta verso il bordo opposto.

## Variazioni sul tema

È possibile introdurre ulteriori elementi per rendere più elaborato il modello.
A titolo di esempio:

- Mostrare l'andamento nel tempo della distribuzione dei boids nel piano con degli istogrammi.

- Cambiare il modo in cui vengono individuati i vicini fornendo ai boids un angolo di vista. [esempio](http://www.red3d.com/cwr/boids/images/neighborhood.gif)

- Utilizzare una libreria grafica per mostrare il volo dei boids nel piano

- Simulare il comportamento di stormi differenti, limitando le regole di volo ai
  boids appartenenti allo stesso stormo

- Simulare il comportamento di un boid predatore che tende a seguire boids
  appartenenti ad altri stormi, i quali applicheranno su di esso la sola regola
  di separazione

## Suggerimenti sull'implementazione

I parametri $s$, $a$, e $c$ delle regole di volo dipendono dall'implementazione
delle velocità. In linea di principio sono dei fattori di proporzionlaità che
determinano l'influenza di una certa regola sul moto dei boids. Un suggerimento
è provare in partenza con valori compresi tra 0 e 1, e trovare il range che più
si adatta alla propria implementazione.

Il parametro $d$ determina la vicinanza tra boids e di conseguenza l'applicazione delle regole di volo; si consiglia di
scegliere un valore che permetta ai boids di "vedere" i vicini più prossimi. Valori troppo alti risulteranno in voli più
caotici, mentre valori troppo bassi renderebbero i boids "ciechi". In entrambi i casi sarà difficile il formarsi di
stormi.

Il parametro $d_s$ determina la soglia di separazione tra boids, il suo valore
deve essere molto minore del valore $d$ di vicinanza. In tal modo i boids
potranno tenersi vicini al proprio stormo, senza però sovrapporsi.

E' opportuno introdurre un limite alla velocità massima di volo dei boids per
evitare comportamenti anomali che potrebbero rendere difficile la simulazione.
Essendo la simulazione a intervalli di tempo discreti (per forza di cose,
facendo la simulazione su una macchina digitale) dei valori di velocità troppo
alti possono rendere impossibile per i boids "incontrarsi" e quindi adattare il
proprio volo ai vicini.

## Riferimenti utili

- [Boids - wikipedia](https://it.wikipedia.org/wiki/Boids)
- [Pagina di Craig Raynolds sui boids](http://www.red3d.com/cwr/boids/)
