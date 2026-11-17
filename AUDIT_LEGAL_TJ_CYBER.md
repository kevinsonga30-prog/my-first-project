# Audit juridique et confidentialité — TJ CYBER

> **Document de travail pédagogique — 18 novembre 2026.** Ce document n'est pas un avis juridique. Il décrit ce qui a été observé dans le dépôt `kevinsonga30-prog/my-first-project` sur la branche `main`. Il ne certifie pas la conformité du site et ne remplace pas une vérification par un professionnel compétent au Cameroun.

## 1. Périmètre et hypothèses

- Projet examiné : page web statique TJ CYBER, principalement `index.html`, avec `README.md`.
- Le README présente le site comme une démonstration pédagogique sans backend.
- Le code charge des polices depuis Google Fonts et utilise `localStorage` pour les comptes, la session, la progression et la préférence de langue.
- Le pays de l'éditeur, son statut, son identité juridique, son public cible réel et les conditions exactes d'hébergement doivent encore être confirmés. Le contexte de travail est le Cameroun ; cela ne suffit pas à conclure à lui seul sur toutes les règles applicables.
- Aucun paiement ni traitement de commande côté serveur n'a été identifié dans le code examiné. La présence d'une rubrique « Tarifs » ne prouve pas qu'une vente est effectivement proposée.

## 2. Cadre juridique camerounais à prendre en compte

1. **Données personnelles :** la loi camerounaise n° 2024/017 du 23 décembre 2024 porte sur la protection des données à caractère personnel. Son champ couvre notamment des traitements effectués par des personnes physiques ou morales et des traitements concernant des personnes établies, résidant ou en transit au Cameroun. Le délai de mise en conformité de 18 mois mentionné à l'article 73 conduit au 23 juin 2026 ; à la date de ce document, il est dépassé. Il faut vérifier le texte intégral, les éventuels textes d'application et la situation de l'autorité compétente avant toute mise en production.
2. **Commerce électronique :** la loi n° 2010/021 du 21 décembre 2010 régit le commerce électronique au Cameroun. Elle prévoit notamment des informations précontractuelles pour les transactions commerciales électroniques et des conditions contractuelles accessibles et conservables. Les obligations exactes dépendront du fait que TJ CYBER vende réellement un service ou un produit.
3. **Cybersécurité :** la loi n° 2010/012 du 21 décembre 2010 relative à la cybersécurité et à la cybercriminalité fait partie du cadre national pertinent. Ce document ne tente pas d'en tirer une conclusion juridique exhaustive.

**Sources officielles et de référence à relire :**
- Présidence de la République du Cameroun — loi n° 2024/017 : https://www.prc.cm/fr/actualites/actes/lois/7588
- CamGovCA / ANTIC — textes de référence, dont les lois n° 2010/012 et n° 2010/021 : https://www.camgovca.cm/en/regulation-policy/laws-and-regulations.html
- Texte de la loi n° 2010/021 sur le commerce électronique : https://www.camgovca.cm/images/downloads/articles/Loi%20sur%20le%20commerce%20%C3%A9lectronique%20-%2021-12-2010.pdf

## 3. Constat du code — état observé

### A. Comptes et données personnelles — À TRAITER

Dans `index.html` :
- Le formulaire d'inscription demande un nom complet, un identifiant ou e-mail, un mot de passe et sa confirmation.
- Les comptes sont enregistrés dans `localStorage` sous `tj-users`, avec identifiant, nom, sel, empreinte du mot de passe et date de création.
- La session est enregistrée sous `tj-session`.
- La progression est enregistrée sous des clés `tj-prog-...`.
- Le code ne transmet pas ces données à un backend dans le flux d'inscription/connexion observé. Le README décrit aussi une démo sans serveur.
- Le site affirme que les données restent dans le navigateur. Cette phrase doit être nuancée : le navigateur de l'utilisateur conserve les données localement, mais l'hébergement et le chargement de ressources externes impliquent tout de même des échanges réseau ordinaires.

**Risques et améliorations :**
- Le nom, l'identifiant/e-mail, les données de session et de progression peuvent être des données personnelles. Il faut informer clairement l'utilisateur avant l'inscription, expliquer la finalité, le stockage local, la durée, la suppression et les limites de la démonstration.
- Un simple SHA-256 (même avec sel) n'est pas un mécanisme adapté au stockage de mots de passe en production. Le repli FNV du code est encore moins adapté. Pour une vraie authentification, ne pas conserver de comptes dans le navigateur : utiliser un backend sécurisé et un mécanisme de hachage de mot de passe conçu à cet effet. Pour la démo actuelle, éviter d'utiliser un vrai mot de passe ou une adresse e-mail réelle.
- Prévoir une fonction claire pour effacer le compte et les données locales, ou indiquer comment l'utilisateur peut les supprimer.
- Ajouter des limites d'âge et un parcours adapté si le service s'adresse à des mineurs ; ne pas collecter de données inutiles.

### B. Scripts et services tiers — À VÉRIFIER

- Deux ressources Google Fonts sont référencées : une préconnexion à `fonts.googleapis.com` et une feuille de style Google Fonts.
- Aucun script d'analyse, pixel publicitaire, iframe vidéo, outil de chat, SDK de paiement ou appel réseau de compte n'a été repéré dans le code examiné.
- Le chargement de Google Fonts peut communiquer au fournisseur des informations techniques telles que l'adresse IP et les caractéristiques de la requête. Vérifier les conditions actuelles du fournisseur et décider si l'on conserve les polices externes ou si l'on héberge les fichiers de police localement.
- Ne pas ajouter de bandeau cookies automatiquement : aucun traceur publicitaire ou analytique non essentiel n'a été repéré dans le code examiné. Il faut néanmoins vérifier le comportement réel du site et de l'hébergeur dans un navigateur avant de conclure.

### C. Informations légales existantes — À CORRIGER / CONFIRMER

Le pied de page comporte des liens vers « Mentions légales » et « Politique de confidentialité », mais ils ouvrent actuellement une même fenêtre modale avec un texte combiné. Les liens CGV et charte d'usage pointent vers une fonction « bientôt disponible ».

Le texte actuel indique notamment :
- « TJ CYBER Academy — projet pédagogique étudiant » ;
- « TJ, étudiant·e en première année » comme responsable de publication ;
- GitHub Pages / GitHub Inc. comme hébergeur ;
- un stockage local des comptes, scores et préférences.

Points à vérifier :
- Confirmer l'identité réelle de l'éditeur et du responsable de publication, sans publier d'adresse personnelle inutile.
- Confirmer l'hébergeur réellement utilisé et ses coordonnées officielles à jour. Ne pas recopier une adresse trouvée dans un ancien modèle sans vérification.
- Séparer les mentions légales de la politique de confidentialité et rendre les deux documents consultables et imprimables.
- La mention « RGPD » seule ne suffit pas à décrire le cadre camerounais.
- Le pied de page affiche aussi des affirmations telles que « fondée en 2019 », « formations certifiantes Qualiopi », « instructeurs opérationnels » et « PARIS / LYON / DISTANT ». Elles doivent être prouvées ou supprimées si elles ne correspondent pas à la réalité. Qualiopi est une référence française et ne doit pas être revendiquée sans certification valable.

### D. Vente, CGV et médiation — NON CONFIRMÉ

- Une section « Tarifs » est présente, mais aucun système de paiement ou de commande n'a été identifié dans le code examiné.
- Tant que le site ne vend rien et ne prend aucune commande, ne pas inventer des CGV ou un médiateur.
- Si une vente en ligne est ajoutée, revoir la loi camerounaise sur le commerce électronique : identité et coordonnées du vendeur, caractéristiques et prix, modalités de paiement, livraison/exécution, garanties, réclamations, retours et informations précontractuelles adaptées au service réel.
- Ne pas transposer automatiquement le délai français de rétractation de 14 jours ni le dispositif français de médiation à un site établi au Cameroun.

### E. Formulaires — À AMÉLIORER

- Le formulaire de connexion et le formulaire d'inscription sont présents.
- Les champs de formulaire ont des éléments `label`, mais les labels observés ne comportent pas d'attribut `for` associé aux identifiants des champs. Corriger l'association pour l'accessibilité.
- Ajouter une information courte, visible avant l'inscription, expliquant les données demandées et le stockage local.
- La case de consentement n'est pas automatiquement nécessaire pour chaque traitement : déterminer la base juridique appropriée avec le texte camerounais et ne demander un consentement explicite que lorsqu'il est requis.

### F. Accessibilité — PREMIER CONTRÔLE

- Des labels visuels existent, mais leur association technique avec les champs doit être corrigée.
- Réaliser un contrôle complet du contraste, du clavier, du focus visible, des titres, des textes alternatifs des images et de l'affichage mobile.
- Le présent audit n'établit pas que le site est conforme à un référentiel précis.

### G. Visibilité auprès des agents IA — OPTIONNEL

- Le site possède déjà une langue HTML, un titre et une méta-description.
- Aucun fichier `robots.txt`, `sitemap.xml` ou `llms.txt` n'a été confirmé dans le contenu examiné.
- On pourra ajouter ces fichiers si le propriétaire souhaite rendre le contenu public plus facile à découvrir. Ne pas ouvrir l'accès à des données privées ou à des espaces de compte.

## 4. Checklist adaptée au projet

- [ ] Confirmer le pays d'établissement et le statut de l'éditeur.
- [ ] Confirmer si TJ CYBER est une démonstration scolaire, un portfolio ou un service réellement exploité.
- [ ] Confirmer si des utilisateurs réels peuvent s'inscrire et quel public est visé.
- [ ] Réécrire les mentions légales avec des informations exactes et vérifiées.
- [ ] Rédiger une politique de confidentialité correspondant aux données réellement manipulées.
- [ ] Expliquer le stockage local et proposer une suppression claire des données de démonstration.
- [ ] Ne jamais présenter l'authentification actuelle comme sécurisée pour une production réelle.
- [ ] Décider si Google Fonts reste externe ou est hébergé localement.
- [ ] Tester les cookies et stockages réellement utilisés dans le navigateur avant de décider si un bandeau est nécessaire.
- [ ] Vérifier les affirmations commerciales et retirer celles qui ne sont pas démontrables.
- [ ] Corriger les labels des formulaires et effectuer un audit d'accessibilité.
- [ ] Si une vente est ajoutée, préparer les informations contractuelles camerounaises avant d'activer les paiements.
- [ ] Faire vérifier les documents par un professionnel compétent avant une exploitation commerciale.

## 5. Informations humaines à confirmer avant toute modification juridique

1. Le projet est-il uniquement un exercice pédagogique ou comptes-tu le rendre accessible au public ?
2. L'éditeur est-il établi au Cameroun ? Sous quel statut (particulier, entreprise, association ou autre) ?
3. Le site est-il destiné aux étudiants, au grand public, aux clients payants ou à plusieurs de ces groupes ?
4. Les inscriptions sont-elles réellement ouvertes à des personnes extérieures ?
5. Souhaites-tu vendre des formations ou abonnements, maintenant ou plus tard ?
6. Confirmes-tu que GitHub Pages est toujours l'hébergeur de production ?

## 6. Limites de cet audit

Cet examen porte sur les fichiers consultés du dépôt et sur le code visible. Il ne vérifie pas les journaux internes de GitHub Pages, les paramètres de compte du fournisseur, les cookies posés par le navigateur, les contrats conclus avec des prestataires, ni les lois étrangères éventuellement applicables selon le public ciblé. Les constats doivent être revalidés avant toute mise en ligne publique ou activité commerciale.
