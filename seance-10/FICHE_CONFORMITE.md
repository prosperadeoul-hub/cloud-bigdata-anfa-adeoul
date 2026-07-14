# Fiche de conformité — Application mobile passagers Anfa

> Gabarit fourni. Complétez chaque section **en 2-4 lignes**, en vous appuyant sur le CM.
> Il n'y a pas de "bonne réponse" unique sur certains points — l'important est le raisonnement.

## 1. Finalité du traitement
La collecte de la position GPS sert uniquement à localiser le passager en temps réel pour lui proposer l'itinéraire et l'arrêt le plus proche. Le numéro de téléphone sert d'identifiant unique pour la création du compte, tandis que l'historique de paiement mobile money sert exclusivement à valider, facturer et renouveler les abonnements de transport.

## 2. Données collectées et leur sensibilité
Les données collectées sont la position GPS en temps réel, l'historique de paiement mobile money et le numéro de téléphone. L'historique de paiement et la géolocalisation continue sont les données les plus sensibles : la première révèle la situation financière de l'utilisateur et ses habitudes de consommation, tandis que la seconde permet de retracer l'intégralité de ses déplacements physiques et sa vie privée.

## 3. Base légale applicable
Le traitement des données personnelles est régi par la Loi n° 2019-014 relative à la protection des données à caractère personnel au Togo. Pour la partie transactions financières et identification mobile money, la Loi n° 2017-007 sur les transactions électroniques s'applique également afin d'assurer la sécurité des paiements et la traçabilité des opérations bancaires mobiles.

## 4. Durée de conservation
Les données de géolocalisation doivent être supprimées immédiatement après la fin du trajet (ou conservées sous forme agrégée et anonymisée). Le numéro de téléphone est conservé tant que le compte est actif, et les données de transaction mobile money sont conservées durant la période légale requise par la réglementation financière (généralement 5 à 10 ans), respectant ainsi le principe de minimisation en limitant le stockage au strict nécessaire métier.

## 5. Hébergement et souveraineté
Pour se conformer à la souveraineté numérique prônée par la loi togolaise, ces données sensibles doivent être hébergées sur le territoire national (par exemple dans le datacenter d'Anfa ou un cloud togolais). Un hébergement chez un fournisseur cloud américain exposerait ces données au Cloud Act et au Patriot Act, permettant aux autorités américaines d'exiger l'accès aux données des citoyens togolais sans l'accord préalable du Togo.

## 6. Droit des personnes concernées
Oui, le passager dispose d'un droit de suppression de ses données. Techniquement, l'architecture construite depuis la séance 1 ne permet pas une suppression facile et ciblée, car supprimer des lignes spécifiques dans des fichiers de logs stockés de manière immuable ou distribuée requiert des processus lourds de réécriture complète des fichiers de données.
