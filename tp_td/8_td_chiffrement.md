# Exercice — Chiffrer et déchiffrer un message à la main (chiffrement asymétrique)

## Objectif pédagogique

Cet exercice a pour but de **manipuler concrètement le chiffrement asymétrique**, sans ordinateur, afin de :

- Comprendre le rôle d’une **clé publique** et d’une **clé privée**
- Comprendre que **chiffrer et déchiffrer sont deux opérations différentes**
- Visualiser pourquoi **la clé privée doit rester secrète**
- Faire le lien avec le fonctionnement réel de TLS (RSA simplifié)

**Attention**
Les nombres utilisés ici sont volontairement petits et **TOTALMENT non sécurisés**.
Ils servent uniquement à des fins pédagogiques.

---

## Contexte de l’exercice

- Alice veut recevoir un message secret.
- Bob veut envoyer un message à Alice.
- Tout le monde peut voir les messages chiffrés.
- **Seule Alice doit pouvoir lire le message.**

---

# PARTIE 1 — Génération des clés (donnée à l’étudiant)

Pour simplifier, **les clés sont déjà générées**.

### Clé publique d’Alice
- \( n = 33 \)
- \( e = 3 \)

=> Clé publique = **(e = 3, n = 33)**
=> Cette clé peut être **partagée publiquement**

---

### Clé privée d’Alice
- \( d = 7 \)

=> Clé privée = **d = 7**
=> Cette clé doit rester **secrète**

---

## Rappel des formules

### Chiffrement (clé publique)
\[
C = M^e % n
\]

### Déchiffrement (clé privée)
\[
M = C^d % n
\]

Où :
- \( M \) = message clair (nombre)
- \( C \) = message chiffré

---

# PARTIE 2 — Codage du message

Pour éviter les lettres, on utilise un **codage numérique simple** :

| Lettre | Valeur |
|------|-------|
| A | 1 |
| B | 2 |
| C | 3 |
| ... | ... |
| Z | 26 |

---

### Message à envoyer

Bob veut envoyer à Alice la lettre :

C


Valeur numérique :

C = 3


---

# PARTIE 3 — Chiffrement par Bob (clé publique)

Bob utilise **la clé publique d’Alice**.

### Calcul

\[
C = 3^3 % 33
\]

Étapes :
- \( 3^3 = 27 \)
- \( 27 % 33 = 27 \)

=> **Message chiffré envoyé par Bob :**

27


---

### Question 1

1. Bob connaît-il la clé privée d’Alice ?
2. Bob peut-il déchiffrer lui-même le message qu’il a envoyé ?

---

# PARTIE 4 — Interception du message (attaquant)

Un attaquant intercepte le message :

27


Il connaît :
- la clé publique (3, 33)
- le message chiffré (27)

### Question 2

1. Peut-il retrouver facilement le message original ?
2. Que lui manque-t-il ?

---

# PARTIE 5 — Déchiffrement par Alice (clé privée)

Alice utilise **sa clé privée**.

### Calcul

\[
M = 27^7 % 33
\]

Calcul guidé :

- \( 27^2 % 33 = 3 \)
- \( 27^4 % 33 = 9 \)
- \( 27^7 = 27^4 \times 27^2 \times 27 \)
- \( 9 \times 3 \times 27 = 729 \)
- \( 729 % 33 = 3 \)

=> Message déchiffré :

3 → C


---

### Question 3

1. Pourquoi Alice est-elle la seule à pouvoir retrouver le message ?
2. Que se passerait-il si quelqu’un obtenait la clé privée ?

---

# PARTIE 6 — Travail en binôme

## Exercice 2 — Message personnalisé

1. Choisissez un message court a envoyer a votre binome (moins de 8 lettres)
2. Convertissez chaque lettre en nombre
3. Chiffrez-la avec la clé publique
4. Échangez uniquement le message chiffré avec un autre binôme
5. Déchiffrez avec la clé privée fournie

---

# PARTIE 7 — Mise en perspective TLS

### Question finale

Expliquez en quelques phrases :

- Pourquoi TLS **n’utilise pas ce chiffrement pour toutes les données**
- À quoi sert réellement l’asymétrique dans TLS
- Quel type de clé est utilisé après le handshake

