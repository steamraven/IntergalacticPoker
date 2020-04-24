Notation
- Players: <img src="/tex/691edda89046d376a273f77796d80e32.svg?invert_in_darkmode&sanitize=true" align=middle width=111.44915759999999pt height=21.18721440000001pt/>
- Cards: <img src="/tex/16d391e31190e0adb564350074fd21bd.svg?invert_in_darkmode&sanitize=true" align=middle width=66.69084509999999pt height=21.18721440000001pt/>
- Deals: <img src="/tex/43e8edbafff81d2069687f66304e42dd.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
- Shuffle: <img src="/tex/cdf1db30928f5c194424bae985c740c4.svg?invert_in_darkmode&sanitize=true" align=middle width=67.61717655pt height=21.68300969999999pt/>
- Encrypted Value: <img src="/tex/1e5f5dc29b232bc345d9ce3fb3c4d662.svg?invert_in_darkmode&sanitize=true" align=middle width=87.84869939999999pt height=24.65753399999998pt/>
- Offset < Private Key > : <img src="/tex/332cc365a4987aacce0ead01b8bdcc0b.svg?invert_in_darkmode&sanitize=true" align=middle width=9.39498779999999pt height=14.15524440000002pt/>
- Offset parts < Private Key> : <img src="/tex/0957a9bbf01d2ea5f621f1d068d404d9.svg?invert_in_darkmode&sanitize=true" align=middle width=16.17146519999999pt height=14.15524440000002pt/>
- Keys for each deal: <img src="/tex/7819eb88d9d0a019b83342ade14ff405.svg?invert_in_darkmode&sanitize=true" align=middle width=72.85759139999999pt height=24.65753399999998pt/>
- Key parts for each deal: <img src="/tex/2c804208883166e74560869fbb45d9a4.svg?invert_in_darkmode&sanitize=true" align=middle width=98.63284529999999pt height=24.65753399999998pt/>
- Deck (of encrypted values): <img src="/tex/172ca2489bedb573582a9860e692b740.svg?invert_in_darkmode&sanitize=true" align=middle width=260.8443123pt height=24.65753399999998pt/>
- Eliptical Curve Generator: <img src="/tex/df5a289587a2f0247a5b97c1e8ac58ca.svg?invert_in_darkmode&sanitize=true" align=middle width=12.83677559999999pt height=22.465723500000017pt/>
- Eliptical Curve Identity Element: <img src="/tex/9fa4bf66c871f8af69c9d3cf2fcb6a55.svg?invert_in_darkmode&sanitize=true" align=middle width=13.54343924999999pt height=22.465723500000017pt/>
- Ephemeral keys (Only used in that step): <img src="/tex/3cf87ea38a615ed99e0232f8ed9431fe.svg?invert_in_darkmode&sanitize=true" align=middle width=12.067218899999991pt height=14.15524440000002pt/>
- Decrypt Function   
  <img src="/tex/3246ab3b8bd2024231938140dd1c8845.svg?invert_in_darkmode&sanitize=true" align=middle width=143.43616815pt height=24.65753399999998pt/>  
- Private Key Generation Function: <img src="/tex/48c029f5527189e81c3e7d50abeb7348.svg?invert_in_darkmode&sanitize=true" align=middle width=107.98363124999997pt height=24.65753399999998pt/>

## Setup
### Request Deal Parts

#### Calc:
- Generate dealer's part of each deal keys:  
  for <img src="/tex/d05dbb83e8409c1f76861680a55c2f19.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
  <img src="/tex/7531fc334175e4c6e9a6436e4834cd30.svg?invert_in_darkmode&sanitize=true" align=middle width=154.38667364999998pt height=24.65753399999998pt/>
- Generate dealer's part of each deal public keys:  
  for <img src="/tex/d05dbb83e8409c1f76861680a55c2f19.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
  <img src="/tex/2b8fe067d00e3cff471ac3a39949c5ef.svg?invert_in_darkmode&sanitize=true" align=middle width=49.19416919999998pt height=22.831056599999986pt/>
- Generate Dealer's Shuffle Offset private key  
  <img src="/tex/bffb0ab0ae1664a895a1010b8e63e3e6.svg?invert_in_darkmode&sanitize=true" align=middle width=203.88089369999997pt height=24.65753399999998pt/>

#### Message:
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`requestDealParts`>
- `players`: `List[PlayerInfo]` | <img src="/tex/65567a15e4e031371b63e97b853f8c6d.svg?invert_in_darkmode&sanitize=true" align=middle width=119.11480845pt height=24.65753399999998pt/>
- `deck`: `DeckInfo`
- `cards`: `int` | <img src="/tex/11f29671c9a023d84560a9a7ca22d779.svg?invert_in_darkmode&sanitize=true" align=middle width=15.74152799999999pt height=14.15524440000002pt/>  
    e.g.: 52
- `shuffleOrder`: `List[int]` | <img src="/tex/84f0072e1e495e1d82f552fbd11ece0b.svg?invert_in_darkmode&sanitize=true" align=middle width=168.52846889999998pt height=24.65753399999998pt/>
- `dealPublicKeyParts`: `List[PublicKey]` | <img src="/tex/f139a9c1dd835a4c8247de98d1811e22.svg?invert_in_darkmode&sanitize=true" align=middle width=155.15049329999997pt height=27.945406500000026pt/>

### Respond Deal Parts
For each player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/> for <img src="/tex/da86900959e9ea0357986bda8282aa77.svg?invert_in_darkmode&sanitize=true" align=middle width=61.97295554999999pt height=21.18721440000001pt/>

#### Calc for each <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>:

- Generate Player's part of each deal keys:  
  for <img src="/tex/d05dbb83e8409c1f76861680a55c2f19.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
  <img src="/tex/d55bb603c811c28f560ed3f97dbb2e39.svg?invert_in_darkmode&sanitize=true" align=middle width=154.61059019999996pt height=24.65753399999998pt/>
- Generate Player's Part of each deal public key:  
  for <img src="/tex/d05dbb83e8409c1f76861680a55c2f19.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
  <img src="/tex/e77db738b3104f2d579f52473abc8367.svg?invert_in_darkmode&sanitize=true" align=middle width=49.418084099999994pt height=22.831056599999986pt/> 
- generate shuffle offset key  
  <img src="/tex/15d8f70f2affa7393a436dad2c3b2e1a.svg?invert_in_darkmode&sanitize=true" align=middle width=204.10481024999996pt height=24.65753399999998pt/>

#### Message for each <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>:

- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`respondDealParts`>
- `playerId`: `int` | <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- `dealPublicKeyParts`: `List[PublicKey]` | <img src="/tex/fb2d2dab055877fea8939e889b24c103.svg?invert_in_darkmode&sanitize=true" align=middle width=155.3744082pt height=27.945406500000026pt/>


## Shuffing
### Shuffle Setup 
For player <img src="/tex/20f392dc03f0f9ec828981c1954ed90c.svg?invert_in_darkmode&sanitize=true" align=middle width=158.96992649999999pt height=24.65753399999998pt/>

####  Calc For player <img src="/tex/e48fedf0490f51b6457b8c979bc10c27.svg?invert_in_darkmode&sanitize=true" align=middle width=14.823113249999992pt height=14.15524440000002pt/>
- Create a public key for each deal by combining all parts from players  
<img src="/tex/f46e17bc0e8cceed1303ebba9ad41ac8.svg?invert_in_darkmode&sanitize=true" align=middle width=154.4068251pt height=27.716805599999994pt/>
- Generate ephimeral keys  
for <img src="/tex/d05dbb83e8409c1f76861680a55c2f19.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
<img src="/tex/2fefb6aa8ebda8d3e95c35a53e5d23a3.svg?invert_in_darkmode&sanitize=true" align=middle width=142.79037959999997pt height=24.65753399999998pt/> 
- Use the combined deal keys to encrypt identity element  
<img src="/tex/00cba8b12cc987d522a63b343369aab9.svg?invert_in_darkmode&sanitize=true" align=middle width=192.70135829999998pt height=24.65753399999998pt/>
- Assemble deck  
<img src="/tex/5044cac72fd77e9cff3cafaba4680abe.svg?invert_in_darkmode&sanitize=true" align=middle width=188.73496124999997pt height=27.945406500000026pt/>


### Shuffle steps
In sequence, each shuffle step <img src="/tex/3015fe34161648241499a598295f981f.svg?invert_in_darkmode&sanitize=true" align=middle width=67.61717655pt height=21.68300969999999pt/> is performed by the designated player <img src="/tex/4235df723e1b24cf0b0ef2453cbdc776.svg?invert_in_darkmode&sanitize=true" align=middle width=158.0130783pt height=24.65753399999998pt/>


#### Calc for each step <img src="/tex/36b5afebdba34564d884d347484ac0c7.svg?invert_in_darkmode&sanitize=true" align=middle width=7.710416999999989pt height=21.68300969999999pt/> for player <img src="/tex/7f131a60c8e7bb2b22f383f7bd49e2c0.svg?invert_in_darkmode&sanitize=true" align=middle width=14.37507554999999pt height=14.15524440000002pt/>
- Generate private, ephemeral, re-encryption keys  
  for <img src="/tex/d05dbb83e8409c1f76861680a55c2f19.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
<img src="/tex/ce6c7ddec776a4a56076dfcca873d2fe.svg?invert_in_darkmode&sanitize=true" align=middle width=200.00056395pt height=24.65753399999998pt/>

- Re-encrypt and offset each card  
for <img src="/tex/43e8edbafff81d2069687f66304e42dd.svg?invert_in_darkmode&sanitize=true" align=middle width=65.2402674pt height=21.68300969999999pt/>  
<img src="/tex/5a516a6958a5a56e0e2cfc26804be89f.svg?invert_in_darkmode&sanitize=true" align=middle width=105.49130459999999pt height=24.65753399999998pt/>  
<img src="/tex/e901efcc69336b6c995726d500075d72.svg?invert_in_darkmode&sanitize=true" align=middle width=219.93903359999996pt height=24.65753399999998pt/>  
<img src="/tex/0f2cb94b1952ee684442a0971f996663.svg?invert_in_darkmode&sanitize=true" align=middle width=180.67648334999998pt height=27.945406500000026pt/>

- Shuffle Deck  
<img src="/tex/e67e93a7eaac8705bfe896cc2bca36d0.svg?invert_in_darkmode&sanitize=true" align=middle width=279.8399505pt height=24.65753399999998pt/>

#### Message for each step <img src="/tex/36b5afebdba34564d884d347484ac0c7.svg?invert_in_darkmode&sanitize=true" align=middle width=7.710416999999989pt height=21.68300969999999pt/> for player <img src="/tex/7f131a60c8e7bb2b22f383f7bd49e2c0.svg?invert_in_darkmode&sanitize=true" align=middle width=14.37507554999999pt height=14.15524440000002pt/>
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`shuffle`>
- `playerId`: `int` | <img src="/tex/7f131a60c8e7bb2b22f383f7bd49e2c0.svg?invert_in_darkmode&sanitize=true" align=middle width=14.37507554999999pt height=14.15524440000002pt/>
- `step`: `int` | <img src="/tex/36b5afebdba34564d884d347484ac0c7.svg?invert_in_darkmode&sanitize=true" align=middle width=7.710416999999989pt height=21.68300969999999pt/>
- `deck`: `List[Encryption]` | <img src="/tex/c1c9f416b0a5324999a52ac503d08bc5.svg?invert_in_darkmode&sanitize=true" align=middle width=169.30402335pt height=27.945406500000026pt/>


### Finish Shuffle
for each player <img src="/tex/0ab52eec5c84e6ab5986c75c3dea4707.svg?invert_in_darkmode&sanitize=true" align=middle width=64.18320974999999pt height=21.18721440000001pt/>

####  Message for each <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`revealOffset`>
- `playerId`: `int` | <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- `offset`: `int` | <img src="/tex/0957a9bbf01d2ea5f621f1d068d404d9.svg?invert_in_darkmode&sanitize=true" align=middle width=16.17146519999999pt height=14.15524440000002pt/>

#### Calculate for each <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- Calculate combined shuffle offset  
  <img src="/tex/cf481be5f27a3abce915d493bc1148c6.svg?invert_in_darkmode&sanitize=true" align=middle width=91.14039659999999pt height=27.716805599999994pt/>
- Use the last shuffle as the shared deck  
  <img src="/tex/5e5c215279b0001287f379e602570f9e.svg?invert_in_darkmode&sanitize=true" align=middle width=110.85327989999998pt height=22.831056599999986pt/>


## Dealing
### Deal a card to a player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>, initial

#### Message from Dealer
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`dealInitial`>
- `player`: int | <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- `dealNo`: int | <img src="/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/>

### Deal a card to a player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>, finailize
From every other player <img src="/tex/2e1b5dc503e44e9e7112b83b4175d4f0.svg?invert_in_darkmode&sanitize=true" align=middle width=141.7343928pt height=24.65753399999998pt/>

#### Message from player <img src="/tex/4e079981711af695f7622e49de92d0de.svg?invert_in_darkmode&sanitize=true" align=middle width=12.79110854999999pt height=18.264896099999987pt/>
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`dealFinal`>
- `playerId`: int | <img src="/tex/4e079981711af695f7622e49de92d0de.svg?invert_in_darkmode&sanitize=true" align=middle width=12.79110854999999pt height=18.264896099999987pt/>
- `dealNo`: int | <img src="/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/>
- `dealKeyPart`: PrivateKey | <img src="/tex/04e51683110a91eea5fe77fcdb007cf1.svg?invert_in_darkmode&sanitize=true" align=middle width=27.677434949999988pt height=22.831056599999986pt/>


### Deal a card to a player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>, verify

#### Calc for deal <img src="/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/> for player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- Calculate deal private key from all other parts  
  <img src="/tex/4ed6d19892e18cc126ebe0d34eccdb1f.svg?invert_in_darkmode&sanitize=true" align=middle width=141.23356005pt height=27.716805599999994pt/>
- Verify valid deal private key  
  <img src="/tex/687d0865034086b42bbf3d8a8cb8c5d5.svg?invert_in_darkmode&sanitize=true" align=middle width=124.96352879999999pt height=22.831056599999986pt/>
- Find card  
  <img src="/tex/60eead1132e11ef3d34276b07a008ce2.svg?invert_in_darkmode&sanitize=true" align=middle width=277.98693779999996pt height=24.65753399999998pt/>
- Ensure only 1 Card found  
  <img src="/tex/2031704e41090a3e2e14267bd8869697.svg?invert_in_darkmode&sanitize=true" align=middle width=307.7945639999999pt height=24.65753399999998pt/>


## Reveal card
### Reveal a card face-up, initial
####  Message from dealer
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`revealInitial`>
- `dealNo`: int | <img src="/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/>
- `dealKeyPart`: PrivateKey | <img src="/tex/c8cde51933c05884622b4c751483c390.svg?invert_in_darkmode&sanitize=true" align=middle width=29.579083049999987pt height=22.831056599999986pt/>

### Reveal a card face-up, finailize
From every other player <img src="/tex/8f2babcd278e4f92a55744604dccb71f.svg?invert_in_darkmode&sanitize=true" align=middle width=81.58622339999998pt height=24.65753399999998pt/>

#### Message from player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- `system`: `String Literal` <`cards`>
- `type`:  `String Literal` <`revealFinal`>
- `playerId`: int | <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>
- `dealNo`: int | <img src="/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/>
- `dealKeyPart`: PrivateKey | <img src="/tex/53ec6fda988726f217f04412abe65a78.svg?invert_in_darkmode&sanitize=true" align=middle width=23.88747404999999pt height=22.831056599999986pt/>

### Reveal a card, verify
For each player <img src="/tex/2ec6e630f199f589a2402fdf3e0289d5.svg?invert_in_darkmode&sanitize=true" align=middle width=8.270567249999992pt height=14.15524440000002pt/>

- Calculate deal private key from all other parts  
  <img src="/tex/4ed6d19892e18cc126ebe0d34eccdb1f.svg?invert_in_darkmode&sanitize=true" align=middle width=141.23356005pt height=27.716805599999994pt/>
- Verify valid deal private key  
  <img src="/tex/687d0865034086b42bbf3d8a8cb8c5d5.svg?invert_in_darkmode&sanitize=true" align=middle width=124.96352879999999pt height=22.831056599999986pt/>  
- Find card  
  <img src="/tex/60eead1132e11ef3d34276b07a008ce2.svg?invert_in_darkmode&sanitize=true" align=middle width=277.98693779999996pt height=24.65753399999998pt/>
- Ensure only 1 Card found  
  <img src="/tex/2031704e41090a3e2e14267bd8869697.svg?invert_in_darkmode&sanitize=true" align=middle width=307.7945639999999pt height=24.65753399999998pt/>
