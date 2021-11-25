# Piccolo Teorema di Fermat

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

