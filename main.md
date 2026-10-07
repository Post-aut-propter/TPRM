## Plan d’action

### 1. Recenser les tiers, y compris ceux qui échappent aux achats

Établissez une liste initiale en croisant les sources internes plutôt qu’en envoyant un questionnaire :

- achats, contrats, factures et paiements ;
- applications SaaS, annuaires SSO et outils de gestion des appareils ;
- comptes techniques, accès distants, VPN et connexions API ;
- équipes métiers, informatique, sécurité, juridique et comptabilité ;
- prestataires de maintenance pouvant accéder aux locaux, équipements ou réseaux.

Cherchez explicitement le **Shadow IT** : abonnements payés par carte d’entreprise, outils choisis par une équipe et services accessibles sans processus d’achat. Ajoutez aussi, lorsque l’information est disponible, les sous-traitants et dépendances critiques de vos prestataires — les « quatrièmes parties ».

### 2. Identifier les fournisseurs importants par leur impact et leurs accès

Notez chaque fournisseur de **0 à 3** sur ces critères :

| Critère | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| Accès aux systèmes | Aucun | Indirect ou limité | Accès à certains systèmes | Accès privilégié, distant ou étendu |
| Données accessibles | Aucune | Données internes peu sensibles | Données sensibles ou personnelles | Données très sensibles ou grande volumétrie |
| Impact d’une interruption | Négligeable | Gêne limitée | Perturbation importante | Activité critique arrêtée |
| Remplaçabilité | Immédiate | Quelques solutions disponibles | Remplacement difficile | Pas de solution réaliste à court terme |
| Dépendance / concentration | Isolée | Dépendance faible | Plusieurs processus dépendent du service | Dépendance forte ou fournisseur commun à plusieurs services |

Additionnez les notes sur 15. Comme **règle de départ**, classez « important » un fournisseur avec un total d’au moins 8, **ou** un score de 3 en accès aux systèmes, données sensibles ou impact d’interruption. Ajustez les seuils à votre contexte et conservez la justification. Un prestataire de maintenance peut ainsi être important en raison de son accès distant, même s’il ne traite pas de données clients.

### 3. Évaluer les fournisseurs importants par des preuves, pas par des réponses déclaratives

Pour ces fournisseurs, constituez un dossier à partir de preuves internes, contractuelles et indépendantes :

- **Accès :** comptes actifs, privilèges accordés, MFA, connexions distantes, journaux, segmentation, comptes partagés ou inutilisés.
- **Sécurité :** rapports d’audit ou certifications disponibles, avis de vulnérabilité, incidents publics, mesures de sécurité documentées. Une certification est un élément de preuve, pas une garantie d’absence de risque.
- **Contrat :** délai de notification d’incident, lieu de stockage des données, sous-traitance autorisée, droits d’audit ou de vérification, exigences de sécurité, assistance en cas d’incident et modalités de résiliation.
- **Dépendances :** hébergeur, logiciel ou service sous-jacent indispensable, dépendance à un fournisseur commun, possibilité d’impact en cascade.
- **Continuité et sortie :** solution de remplacement, portabilité et récupération des données, durée de transition, capacité à fonctionner en mode dégradé, modalités de suppression des données et preuve de destruction.

Pour chaque constat, consignez la **source, la date et la fiabilité** de la preuve. Si vous ne pouvez pas confirmer un point, notez **« inconnu »** : ne le transformez ni en conformité, ni automatiquement en incident. Quand un grand fournisseur ne permet pas d’audit direct, exploitez ses rapports indépendants et renforcez vos propres mesures de résilience, sauvegarde et continuité.

### 4. Traiter les écarts et préparer la sortie

Associez chaque écart à une action, un responsable, une échéance et une preuve de clôture. Exemples : retirer un compte distant devenu inutile, limiter un accès au strict nécessaire, exiger une clause de notification d’incident au prochain renouvellement, tester la récupération des données ou documenter un mode de fonctionnement dégradé.

Pour les fournisseurs dont la défaillance interromprait une activité importante, formalisez un plan de sortie : alternative envisagée, données à récupérer, étapes de bascule, durée estimée, dépendances à traiter et test de la procédure. Le podcast insiste sur un point pratique : un plan de sortie **non testé** peut ne pas fonctionner le jour où il devient nécessaire.

### 5. Installer une revue continue et proportionnée

Revoyez les fournisseurs importants plus souvent que les autres, ainsi qu’après un incident, une acquisition, un changement de service ou de sous-traitant, une modification d’accès ou une dégradation de la situation. Les résultats doivent être partagés entre sécurité, métier, achats et juridique : le risque ne se règle pas uniquement au moment de signer le contrat.

## Structure du classeur Excel

Je ne peux pas joindre un fichier `.xlsx` depuis cette conversation, mais voici une structure prête à reproduire. Créez quatre onglets : `Fournisseurs`, `Évaluations`, `Actions` et `Synthèse`. Les en-têtes ci-dessous peuvent être copiés dans Excel ; convertissez ensuite chaque plage en tableau avec **Ctrl+T**.

**Onglet `Fournisseurs`** — inventaire, criticité et dépendances :

```text
ID	Nom fournisseur	Service / activité	Propriétaire interne	Source de détection	Accès systèmes (0-3)	Données accessibles (0-3)	Impact interruption (0-3)	Remplaçabilité (0-3)	Dépendance / concentration (0-3)	Score total	Classe	Quatrième partie connue	Contrat localisé ?	Date de revue	Notes / justification
F-001	Exemple SaaS	Paie	Finance	Factures + SSO	2	3	3	2	2	=SOMME(F2:J2)	=SI(OU(K2>=8;F2=3;G2=3;H2=3);"Important";"Standard")	Inconnu	Oui	2026-10-08	Données salariés ; vérifier accès et réversibilité
```

**Onglet `Évaluations`** — preuves et constats, une ligne par point vérifié :

```text
ID fournisseur	Domaine	Point vérifié	État	Constat / preuve	Source	Fiabilité (1-3)	Date de preuve	Impact (1-3)	Action nécessaire
F-001	Accès	MFA des comptes prestataire	Inconnu	À vérifier dans les journaux IAM	Journaux IAM	2	2026-10-08	3	Examiner les comptes et connexions distantes
F-001	Contrat	Notification d’incident	À vérifier	Clause non encore examinée	Contrat	3	2026-10-08	3	Revue par achats et juridique
F-001	Continuité	Récupération des données	Inconnu	Aucun test consigné	Équipe métier	1	2026-10-08	3	Documenter et tester l’export
```

Valeurs pratiques pour `État` : `Conforme`, `Écart`, `Inconnu`, `N/A`. Ajoutez une liste déroulante afin d’éviter les variantes d’écriture.

**Onglet `Actions`** — traitement et clôture des risques :

```text
ID action	ID fournisseur	Constat	Risque / décision	Action	Responsable	Date d’ouverture	Échéance	Statut	Date de clôture	Preuve de clôture
A-001	F-001	MFA des accès prestataire non confirmé	Accès privilégié potentiellement insuffisamment protégé	Vérifier MFA, comptes actifs et journaux	Équipe IAM	2026-10-08	2026-11-08	À faire		
A-002	F-001	Sortie non documentée	Dépendance difficile à remplacer	Documenter l’export, l’alternative et le mode dégradé	Finance + IT	2026-10-08	2026-12-08	À faire		
```

**Onglet `Synthèse`** — indicateurs de pilotage :

```text
Indicateur	Formule
Fournisseurs recensés	=NBVAL(Fournisseurs!B:B)-1
Fournisseurs importants	=NB.SI(Fournisseurs!L:L;"Important")
Actions à faire	=NB.SI(Actions!I:I;"À faire")
Actions en cours	=NB.SI(Actions!I:I;"En cours")
Éléments d’évaluation inconnus	=NB.SI(Évaluations!D:D;"Inconnu")
Actions en retard	=NB.SI.ENS(Actions!H:H;"<"&AUJOURDHUI();Actions!I:I;"<>Clôturée")
```

Selon votre version d’Excel, les noms de fonctions ou séparateurs peuvent varier. Ajoutez une mise en forme conditionnelle pour signaler les échéances dépassées et les fournisseurs importants.

La transcription met particulièrement l’accent sur cinq angles à garder visibles dans le suivi : **accès fournisseur**, **continuité**, **concentration**, **sous-traitance en cascade** et **réversibilité**. Elle rappelle également qu’un fournisseur peut présenter un risque élevé par ce qu’il peut atteindre, et pas seulement par les données qu’il traite.
