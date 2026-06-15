# Entreposage Saint-Tite — Site web

Site vitrine statique géré par **Gestion Pilier**.
Réservation en ligne assurée par le logiciel **Anémone** (Rocksoft) du propriétaire.

## Fiche technique

| Élément | Valeur |
|---|---|
| Client | Entreposage Saint-Tite |
| Domaine | entreposagesttite.ca |
| Registraire du domaine | GoDaddy |
| Hébergement | Railway (projet « Sites clients — Gestion Pilier ») |
| Service Railway | entreposage-saint-tite |
| Dépôt GitHub | entreposage-saint-tite |
| Réservation en ligne | **Anémone** (Rocksoft) — voir branchement ci-dessous |
| Formulaire de contact | Web3Forms (questions générales seulement) |
| Mise en ligne | _(date)_ |
| Frais de gestion mensuels | _(montant)_ |

## ⚠️ À compléter avant la mise en ligne

Le site contient **deux jetons** à remplacer :

| Jeton | Où | Comment l'obtenir |
|---|---|---|
| `{{ANEMONE_RESERVATION_URL}}` | section `#reserver` de `index.html` | Adresse de réservation fournie par **Rocksoft** (voir branchement) |
| `VOTRE_CLE_WEB3FORMS_ICI` | formulaire de contact (section `#contact`) | Clé générée sur web3forms.com avec info@entreposagesttite.ca |

## Branchement de la réservation Anémone

La section « Réserver » est prête pour les **trois façons** dont Rocksoft peut livrer
la réservation en ligne. Choisir selon leur réponse :

| Si Rocksoft fournit… | Quoi faire dans `index.html` |
|---|---|
| **Un lien** vers une page hébergée par Anémone | Remplacer `{{ANEMONE_RESERVATION_URL}}` par ce lien. Terminé. |
| **Un sous-domaine** (ex. `reservation.entreposagesttite.ca`) | Configurer le DNS chez GoDaddy, puis mettre ce sous-domaine dans `{{ANEMONE_RESERVATION_URL}}`. |
| **Un code à intégrer** (widget / iframe) | Dans la section `#reserver` : retirer le bloc `<a>` du bouton, décommenter le bloc `<iframe>` (OPTION B) et y coller le code de Rocksoft. |

Tous les boutons « Réserver » du site (nav, hero, tarifs, bannière) pointent déjà vers
cette section — aucune autre modification nécessaire.

## Questions à poser à Rocksoft

- Le client a-t-il (ou peut-il activer) le module Réservation en ligne et Paiement en ligne d'Anémone Storage?
- Comment la réservation se branche-t-elle à un site web : lien, widget/iframe, ou sous-domaine?
- Peut-on personnaliser l'apparence (logo, couleurs) de la page de réservation?
- Y a-t-il un coût mensuel additionnel?

## Architecture

- HTML statique, page unique (`index.html`), servi par nginx (`nginx:alpine`) sur le port 8080
- Aucune base de données : la réservation, le paiement, le contrat et le contrôle d'accès
  (cartes magnétiques) restent gérés par Anémone
- Le rôle de Gestion Pilier se limite à la vitrine et au branchement

## Fichiers

```
index.html      Site complet (HTML + CSS intégré)
Dockerfile      Image nginx pour Railway
nginx.conf      Config serveur (port 8080)
robots.txt      Indexation
sitemap.xml     Plan du site
assets/img/     Logo, favicon, photos
```
