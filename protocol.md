Notation
- Players: $`p, p\prime, p_s = 1...n_p$
- Cards: $`c = 1...n_c$
- Deals: $`i = 1...n_c`$  
- Shuffle: $`j = 1...n_s$
- Encrypted Value: $`C, C_{j,i} = (\Alpha, \Beta)$
- Offset < Private Key > : $`x$
- Offset parts < Private Key> : $`x_p$
- Keys for each deal: $`(d_i, d_i \cdot P)$
- Key parts for each deal: $`(d{_p,i}, d_{p,i} \cdot P )$
- Deck (of encrypted values): $`Deck, Deck_j, Deck\prime = [C_c | c = 1...n_c]$
- Eliptical Curve Generator: $`P$
- Eliptical Curve Identity Element: $`\mathcal{O}$
- Ephemeral keys (Only used in that step): $`r_i$
- Decrypt Function   
  $`decrypt((\Alpha, \Beta), k): \Alpha - k \cdot \Beta`$  
- Private Key Generation Function: $`generateKey()$

## Setup
### Request Deal Parts

#### Calc:
- Generate dealer's part of each deal keys:  
  for $`i=1...n_c`$  
  $`d_{1,i} = generateKey()$
- Generate dealer's part of each deal public keys:  
  for $`i=1...n_c`$  
  $`d_{1,i} \cdot P$
- Generate Dealer's Shuffle Offset private key  
  $`x_1 = generatePrivateKey()$

#### Message:
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`requestDealParts`>
- `players`: `List[PlayerInfo]` | $`\mid players\mid == n_p$
- `deck`: `DeckInfo`
- `cards`: `int` | $`n_c`$  
    e.g.: 52
- `shuffleOrder`: `List[int]` | $`\mid shuffleOrder \mid == n_s$
- `dealPublicKeyParts`: `List[PublicKey]` | $`\big[\,d_{0,ij} \cdot P \;\big|\; i = 1...n_c\,\big]$

### Respond Deal Parts
For each player $`p`$ for $`p = 2...n$

#### Calc for each $`p$:

- Generate Player's part of each deal keys:  
  for $`i=1...n_c`$  
  $`d_{p,i}= generateKey()$
- Generate Player's Part of each deal public key:  
  for $`i=1...n_c`$  
  $`d_{p,i} \cdot P`$ 
- generate shuffle offset key  
  $`x_p = generatePrivateKey()$

#### Message for each $`p$:

- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`respondDealParts`>
- `playerId`: `int` | $`p$
- `dealPublicKeyParts`: `List[PublicKey]` | $`\big[\,d_{p,ij} \cdot P \;\big|\; i = 1...n_c\,\big]$


## Shuffing
### Shuffle Setup 
For player $`p_1 = shuffleOrder[1]$

####  Calc For player $`p_1$
- Create a public key for each deal by combining all parts from players  
$d_i \cdot P = \sum_{p=1}^{n_p} d_{p,i} \cdot P$
- Generate ephimeral keys  
for $`i=1...n_c`$  
$r_i =  generateKey()`$ 
- Use the combined deal keys to encrypt identity element  
$C_{0,i} = (r_i \cdot (d_i \cdot P)\;,\; r_i \cdot P )$
- Assemble deck  
$Deck_0 = \big[C_{0,i} \;\big|\; i = 1...n_c\big]$


### Shuffle steps
In sequence, each shuffle step $`j=1...n_s`$ is performed by the designated player $`p_j = shuffleOrder[j]$


#### Calc for each step $`j`$ for player $`p_j$
- Generate private, ephemeral, re-encryption keys  
  for $`i=1...n_c`$  
$r_i = generatePrivateKey()$

- Re-encrypt and offset each card  
for $`i = 1...n_c`$  
$(\alpha. \beta) = C_{j-1,\,i}`$  
$C_{j,i} = (r_i \cdot \alpha + r_i x_p \cdot \beta\;,\; r_i \cdot \beta )`$  
$Deck\prime = \big[C_{j,i} \;\big|\; i = 1..n_c \big]$

- Shuffle Deck  
$Deck_j = RandomPermutation(Deck\prime)$

#### Message for each step $`j`$ for player $`p_j$
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`shuffle`>
- `playerId`: `int` | $`p_j$
- `step`: `int` | $`j$
- `deck`: `List[Encryption]` | $`\big[\,(\alpha_{j,i},\beta_{j,i}) \;\big|\; i = 1...n_c\,\big]$


### Finish Shuffle
for each player $`p = 1..n_p$

####  Message for each $`p$
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`revealOffset`>
- `playerId`: `int` | $`p$
- `offset`: `int` | $`x_p$

#### Calculate for each $`p$
- Calculate combined shuffle offset  
  $`x = \sum_{q=1}^{n_p} x_q$
- Use the last shuffle as the shared deck  
  $`Deck = Deck_{n_s}$


## Dealing
### Deal a card to a player $`p$, initial

#### Message from Dealer
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`dealInitial`>
- `player`: int | $`p$
- `dealNo`: int | $`i$

### Deal a card to a player $`p$, finailize
From every other player $`p\prime | p\prime = 1...n_p,  p\prime \neq p$

#### Message from player $`p\prime$
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`dealFinal`>
- `playerId`: int | $`p\prime$
- `dealNo`: int | $`i$
- `dealKeyPart`: PrivateKey | $`d_{p\prime,i}$


### Deal a card to a player $`p$, verify

#### Calc for deal $`i`$ for player $`p$
- Calculate deal private key from all other parts  
  $`d_i = x + \sum_{p\prime=1}^{n_p} d_{p\prime, i}$
- Verify valid deal private key  
  $`d_i \cdot P === d_i \cdot P$
- Find card  
  $`c |  c \in [1,n_c], decrypt(Deck[c],d_i) == \mathcal{O}$
- Ensure only 1 Card found  
  $`decrypt(Deck[c\prime],d_i) \neq \mathcal{O} | c\prime \in [1,n_c], c\prime \neq c$


## Reveal card
### Reveal a card face-up, initial
####  Message from dealer
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`revealInitial`>
- `dealNo`: int | $`i$
- `dealKeyPart`: PrivateKey | $`d_{p\prime,0}$

### Reveal a card face-up, finailize
From every other player $`p | p = 2...n_p$

#### Message from player $`p$
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`revealFinal`>
- `playerId`: int | $`p$
- `dealNo`: int | $`i$
- `dealKeyPart`: PrivateKey | $`d_{p, i}$

### Reveal a card, verify
For each player $`p$

- Calculate deal private key from all other parts  
  $`d_i = x + \sum_{p\prime=1}^{n_p} d_{p\prime, i}$
- Verify valid deal private key  
  $`d_i \cdot P === d_i \cdot P`$  
- Find card  
  $`c |  c \in [1,n_c], decrypt(Deck[c],d_i) == \mathcal{O}$
- Ensure only 1 Card found  
  $`decrypt(Deck[c\prime],d_i) \neq \mathcal{O} | c\prime \in [1,n_c], c\prime \neq c$
