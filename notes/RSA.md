# Piccolo Teorema di Fermat

## Altro
Siano a,n,x,y numeri interi con n>= 1 e MCD(a,n) = 1

$\text{Se } x \equiv y \mod{\phi(n)} \rightarrow a^{x} \equiv a^{y} \mod{x}$

$$\begin{array}{c}
x \equiv y \mod{\phi(n)}\\
x \equiv y + k \phi(n)\\
a^{x} = a^{y+k\phi(n)}=a^{y}(a^{\phi(n)})^k\\
a^{\phi(n)} \equiv 1 \mod{n}\\
= a^{4}1^{k}
\end{array}
$$

# Algoritmo di Euclide
MCD fra due numeri

# Algoritmo di Euclide esteso
Calcolare inverso moltiplicativo

MCD(1180,482) = -> 2
- 1180 = 482*2 + 216
- 482 = 216*2 + 50
- 216 = 50*4 + 16
- 50 = 16*3 + 2
- 16 = 2*8 + 0

Mi servono tutti i quozienti tranne l'ultimo

$$\begin{array}{c}
x_0 = 0\\

x_1 = 1\\

x_j = -q_{j-1}*x_{j-1}+x_{j-2}\\

y_0 = 1\\

y_1 = 0\\

y_j = -q_{j-1}*y_{j-1}+y_{j-2}\\
\end{array}$$

MCD(1180,482) = 2 =
- 1180*y + 482*x


$$\begin{array}{c}
x_2 = -q_1*x_1 + x_0
\end{array}$$

L'inverso moltiplicativo
$ax + by = MCD(a,b) = 1$

$by \equiv 1 \mod{a}$

$by = 1 + tot*a$

$yb = 1 \mod{a}$

**NB**: Se avessi un inverso moltiplicativo > 1 durante la fase di decrittazione avrei n modi di decrittare il messaggio diversi!

# RSA

Pub(n,e)
Priv(p,q,d)

p,q sono numeri primi grandi

Lunghezza chiave
- 1024 deprecato
- 2048 consigliati da NIST
- 4096

$d*e \equiv 1 mod \phi(n)$

$e = \text{numero casuale t.c } MCD(e,\phi(n)) = 1$

$n = pq$

## Encryption
$m^{e} = c \mod{n}$

$c^{d} = m \mod{n}$

$(m^{e})^{d}$

Va scelto un numero con bassa entropia (ad esempio se comprassi un dispositivo che utilizza come numero per generare le chiavi la data, avrei n dispositivi che usano lo stesso numero!)

Come si trova?

Perché $2^{16} + 1$?

Risposta:

$m^{e}$

$e = 1000...01 \leftarrow 2^{16} + 1$ è veloce rispetto a per esempio

$e = 1111...11 \leftarrow 2^{16} + 1$ perché moltiplicherei per 2 solo quando ho un `1`

Scelgo questo perché è sufficientemente grande

# Attacchi ad RSA
## Known $\phi{(n)}$
Conosco $n, e, \phi(n)$
$$\begin{array}{c}
n - \phi(n) + 1 =\\
pq - [(p-1)(q-1)]+1 =\\
pq - [pq-p-q+1]+1 = p+q \rightarrow \\ n - \phi(n) + 1 = p+q \text{ (importante)}\\
n = pq \text{ (importante)}\\
ax^2+bx+c\\
x_1x_2 = \frac{c}{a} \rightarrow n = p*q\\
x_1+x_2=-\frac{b}{a} \rightarrow p + q\\
\end{array}$$

Posso costruire un'equazione di secondo grado

$x^2 - (n-\phi(n)+1)x + n = 0$

$x_1,x_2$ = soluzioni dell'equazione di secondo grado la cui somma è = $\frac{-b}{a}$ e prodotto = $\frac{c}{a}$ e questi due numeri sono per forza **p** e **q**

## Esiste un attacco in grado di fattorizzare N
Se sono in grado di recuperare m/4 cifre di d sono in grado di usare degli attacchi

## Common modules attack (CMA, o Attacco dei pigri)
Alice (e_A, n)
Bob (e_B, n)
p,q = n uso una n unica

m^{e_a} \equiv c_1 \mod{n}
m^{e_b} \equiv c_2 \mod{n}

Supponiamo un terzo, Carl, che voglia comunicare con Alice e Bob

Un attaccante si accorge che una parte della chiave pubblica (\mod{n}) di Alice e Bob sono uguali

Quindi prende il cripto testo e verifica:
- MCD(c1, n) = 1

Usando l'algoritmo di Euclide Esteso:

$$\begin{array}{c}

r*e_A+S*e_B = 1\\

(c_{1}^{-1})^{-r}*(c_2)^S\\

=((m^{e_A})^{-1})^{-r}*(m^{e_B})^S\\

=m^{e_Ar}*m^{e_bS}\\

= m^{(e_Ar+e_BS)}\\

\text{Esponente: } 1 \equiv (e_Ar+e_BS) \mod{\phi(n)}\\
\text{Base: } m \mod{n}\\

= m^1
\end{array}$$

### Esempio
n = 33
m = 20

$e_A = 7, e_B =19$

$C_1=m^{e_a} \mod{n} = 26$

$C_2 = m^{e_B} \mod{n} = 5$

r = -8
S = 3

$C_1^{-1} = 14$

$(C_1^{-1})^1*(C_2)^2=20$

## Low Exponent Attack

$(e,n)$

$d*e \equiv 1 \mod{\phi(n)}$

$d \in [1...\phi(n)]$

Se $d < \frac{1}{3}\sqrt[4]{n}$ allora sei sotto attacco (ci si mette poco ad abbettere chiavi anche da 2048 o 4096 bit)

# Short Plaintext Attack
m chiave di DES, per esempio

RSA \rightarrow DES

$2^{56} \approx 10^{17}$ (molto piccolo)

a*b = m 
posso scriverlo come prodotto di due numeri più piccoli 

$a \leq 10^9$

$b \leq 10^9$

$m = 10^{17}$

$c*x^{-e} \mod{n}$

$y^{e} \mod{n}$

Calcolo quindi due vettori da $x,y = 1$ fino a $x,y = 10^{9}$ per ciascuna delle due formule

Finita la computazione, se trovo due numeri uguali nei due vettori allora questi verificano $c*x^{-e} = y^e$ e quindi $c = (x*y)^e$.

Ma solo un numero elevato alla e può darmi $C$, e quel numero è $m$.
Dunque $m = x*y$

## Come evitare l'attacco usando il Padding
Per evitare il Short Plaintext Attack bisogna usare il padding, in particolare OAEP (Optimal Asymmetric Encryption Padding).
Dietro questo padding esiste una funzione che genera dei bit casuali che possono venire inseriti per allungare il plaintext.

### Come usare?


# 


# Misc
MCD(a,n) = d != 1
$ax =\equiv b \mod{n}$

Posso dividere per a ed n per d

$\frac{a}{d}x =\equiv b \mod{\frac{n}{d}}$

$x_o, x_0 + \frac{n}{d}, x_0 + \frac{2n}{d} ... (d-1)\frac{n}{d}$

$12x \equiv 21 \mod{39}$ (esercizio da fare a casa)

# Teorema cinese dei resti
Se noi abbiamo un set di numeri naturali

$r_1 ... r_n$

$MCD(r_i;r_j) = 1$

$\forall i \ne j$

$a_1 ... a_n$

$$\begin{cases}
x \equiv a_n \mod{r_1}\\
...\\
x_n \equiv a_n \mod{r_n}\\
\end{cases}$$

$x = \sum_{i = 1}^{n} a_i*p_i*q_i$

$P = \prod_{i = 1}^{n} r_i$

$P_i = \frac{P}{r_i}$

$Q_i = P_i^{-1} \mod{r_i}$

MCD(P_i; r_i) = 1

È conveniente da usare perché p e q sono piccoli

# Problema del logaritmo discreto

$\alpha^{x} \equiv \beta \mod{p}$

Tecniche per risolverlo
## Baby steps giant steps
Costruire 2 vettori grandi quanto il modulo **p**

Riempire il vettore in qualche modo a sx e dx e vedere se c'è un'informazione comune

Nel primo vettore calcolo $\alpha^{j}$

Nel secondo vettore calcolo $\beta * \alpha^{-NK}$

$a^{j} \equiv \beta*\alpha^{-NK} \mod{p}$

$a^{j-NK} \equiv \beta \mod{p}$

## Tecnica 2
A priori si può fare un ragionamento

Cerco di capire se il numero è pari o dispari
$$\begin{array}{c}
\alpha^{x} \equiv \alpha^y \mod{p}\\

{x} \equiv y \mod{p-1}\\

\alpha^{p-1} \equiv 1 \mod{p}\\

\alpha^{p-1} \\
...\text{altra roba in mezzo}\\
\alpha^{\frac{p-1}{2}} = -1\\
\alpha^{n} \equiv \beta \mod{p}\\

\beta^{\frac{p-1}{2}} \equiv \alpha^{\frac{p-1}{2}x} = (-1 su 6)^x \mod{p}\\

\beta^{\frac{p-1}{2}} \rightarrow cost = (-1)^x \mod{p}

\end{array}$$

E tolgo il 50% dei calcoli, che però eè ininfluente dato che il numero è grandissimo.

## Tecnica 3
Pre-computo dei logaritmi

$\alpha^{k} = \prod_{p_i}^{a_i} \mod{p}$

$k = \log_{a}(\prod_{p_i}^{a_i})$

$= \sum_{a_i}\log_a{p_i} \mod{p-1}$

$\beta = \alpha^{x} \mod{p}$

$\beta * \alpha^r = \prod_{p_i}^{b_i} \mod{p\prod_{p_i}^{a_i}}$ 

r = numero random

$log_x\beta + r log_{\alpha}\alpha = \sum b_ilog_\alpha p_i$

$\log_\alpha\beta = -r + \sum b_ilog_\alpha p_i \mod{p-1}$

$log_\alpha\beta = x$

Finito

C'è un problema dal punto di vista pratico

p = -131

$\alpha = 2$

B = soglia

$p_i = 2,3,5,7$

# Test di primalità
Test di primalità di Fermat (test probabilistico) utilizzando il piccolo teorema di Fermat e viene utilizzato per dire che un numero non è primo

$a^{n-1} \equiv 1 \mod{n}$

Quando un numero passa il test lo passo ad un altro test, ovvero il test di Miller Rabin

CACCA
