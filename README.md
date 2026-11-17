# 🛡️ TJ CYBER — Académie de Cybersécurité

Plateforme de formation en cybersécurité : parcours certifiants, laboratoires sandbox,

défis interactifs et académie de code (Python, C, Batch, JavaScript).

> Projet pédagogique de première année universitaire.

## ✨ Fonctionnalités

- 🎨 Interface immersive : thème à couleurs cycliques (vert → violet → rouge → jaune), pluie de code, grille animée

- 🌍 Bilingue **FR / EN** (choix mémorisé)

- 💻 **Académie de code** : 12 leçons interactives avec coloration syntaxique, bouton copier et quiz de validation

- 🎯 Défis CTF : cryptanalyse (chiffrement de César) et analyse de phishing

- 👤 **Comptes utilisateurs** : inscription / connexion avec mot de passe **hashé SHA-256**

- 📊 **Espace membre** : XP, badges, progression sauvegardée par compte

- 💶 Grille tarifaire interactive (mensuel / annuel)

- 📄 Mentions légales & conformité RGPD (données 100 % locales)

## 🛠️ Technologies

HTML5 · CSS3 (variables CSS, animations) · JavaScript Vanilla (aucune dépendance) · Web Crypto API · localStorage

## 🚀 Lancer le projet

1. Récupérer le fichier `index.html`

2. L'ouvrir dans un navigateur moderne — c'est tout !

## 🔐 Note de sécurité (à lire pour la soutenance)

L'authentification utilise le `localStorage` du navigateur : c'est un choix **pédagogique**

pour démontrer le hashage des mots de passe sans serveur. En production réelle, il faudrait

un backend (PHP/MySQL, Node.js ou Flask), des sessions côté serveur, HTTPS et des protections

(brute-force, CSRF). Les mots de passe ne sont **jamais** stockés en clair.

## 📈 Perspectives

- Backend avec base de données (comptes, progression centralisée)

- Vraies leçons complètes et labs notés

- Paiement (Stripe) et envoi d'e-mails

- Classement CTF inter-étudiants
