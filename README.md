# Apc-2024--Kaggle-LOL
Aquest projecte té com a objectiu desenvolupar un model de machine learning per predir l'outcome (victòria o derrota) d'una partida de *League of Legends* utilitzant dades de Kaggle.

## Descripció del Dataset

El dataset prové de [Kaggle: League of Legends Dataset](https://www.kaggle.com/datasets/datasnaek/league-of-legends) i conté 61 atributs sobre les partides de *League of Legends*. Inclou dades sobre el temps de creació de la partida, la durada, els jugadors, els camps de batalla, els bans, els campions, les torres destruïdes, i altres estadístiques importants durant les partides.

## Objectiu

L'objectiu és crear un model de machine learning que sigui capaç de predir si un equip guanyarà una partida basada en les característiques de la mateixa. El valor a predir és l'atribut `Winner`, que indica quin equip guanya.

## Anàlisi Exploratòria de Dades (EDA)

1. **Atributs numèrics i categòrics**: El dataset conté tant atributs numèrics (com `creationTime` i `gameDuration`) com atributs discrets (com `GameId` i els identificadors de campions). 
2. **Dades Nans**: No s'han detectat valors nuls en el dataset.
3. **Desbalanceig de les dades**: Es va observar que les dades estan desbalancejades en certs atributs.
4. **Relació entre les variables i la classe a predir**: A simple vista, no es va trobar una relació directa entre les característiques de la partida i el resultat (guanyador/perdedor).

## Preprocessament de les Dades

1. **Eliminació d'atributs innecessaris**: 
   - `GameId`: El valor de `GameId` es repeteix per cada partida, per tant no aporta informació per a la predicció.
   - `SeasonId`: Totes les partides són de la mateixa temporada, per tant aquest atribut és constant i no útil.
   - `CreationTime`: Aquest atribut indica quan es va crear la partida, però no aporta informació rellevant sobre el resultat.

2. **Eliminació de valors anòmals**: 
   - `gameDuration`: Les partides amb una durada inferior a 500 segons (és a dir, rendicions molt ràpides) s'han eliminat perquè no representen una partida típica, són partides on un equip s'ha rendit ràpidament.
   - **`firstTower`**: Els valors de `firstTower=0` (cap torre destruïda) han estat substituïts per la moda, ja que els valors 0 podrien indicar una partida interrompuda.

3. **Transformació de campions i summoners**:
   - Els valors `t1_champ1id`, `t1_champ2id`, ... es van substituir pels tipus dels campions corresponents mitjançant un diccionari obtingut a partir de l'arxiu `champion_info`.
   - Es va realitzar una transformació One-Hot Encoding en les columnes acabades en `sum1` i `sum2` per tal de convertir els valors numèrics dels "summoners" en variables binàries. Això ens permet tractar els summoners com atributs independents.

4. **Metrica d'Avaluació**: Com que la classe objectiu (`Winner`) està equilibrada, es va optar per utilitzar l'*accuracy* com a mètrica principal per avaluar el model.

**Autors**:  
Eric Chaves Sánchez - 1633944  
Enric Rodríguez Bafalluy - 1632398
