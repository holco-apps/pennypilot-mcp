# PennyPilot, connecteur MCP pour Pennylane

PennyPilot est un connecteur [MCP](https://modelcontextprotocol.io) édité par **HOLCO** qui permet aux experts-comptables et à leurs équipes d'interroger en langage naturel leurs dossiers **Pennylane** depuis un assistant IA (Claude, ChatGPT, Le Chat).

Ce dépôt publie, par transparence, le **catalogue public des outils de lecture** et la documentation du connecteur. L'implémentation du serveur, les moteurs de révision et la mémoire du cabinet restent propriétaires.

## Révision assistée

Au-delà de la lecture, PennyPilot aide à **réviser** un dossier en langage métier :

- **Révision guidée** : en une demande, le collaborateur obtient une liste d'écarts priorisés par sévérité (cadrage TVA, cut-off, provisions, amortissements, trésorerie, lettrage), chacun qualifié (cause probable, pièce à regarder, comptes concernés).
- **Doctrine vérifiée** : chaque point cite la source officielle (Légifrance, BOFiP) dans la version en vigueur à la date d'arrêté.
- **Mémoire du cabinet** : une décision tranchée une fois est réappliquée au passage suivant et n'est plus resignalée, avec traçabilité (qui, quand, source). La révision ne repart pas de zéro à chaque clôture.
- **Lecture seule de bout en bout** : PennyPilot propose, le cabinet tranche dans son outil comptable.

Ces capacités s'opèrent côté serveur (propriétaire) ; ce dépôt n'en publie que le principe, pas l'implémentation.

## Principe

- **Lecture de votre comptabilité, sans modification.** Aucun outil ne crée, modifie, supprime, lettre ou poste une écriture comptable.
- **45 outils** au total : **41 strictement en lecture**, **4 à effet de bord technique non destructif** (génération d'un fichier d'export, envoi d'un retour à l'éditeur). Le détail par outil est dans [`tools-catalog.json`](./tools-catalog.json), via l'annotation `readOnlyHint`.
- **Audit trail systématique** sur chaque réponse : faits, calculs, hypothèses, limites, sources officielles. De quoi vérifier et citer.
- **Confidentialité** : le jeton Pennylane est chiffré au repos et n'est jamais transmis au modèle. Les données comptables sont lues à la volée, sans cache ni indexation, sans rétention.

## Catalogue des outils

Le fichier [`tools-catalog.json`](./tools-catalog.json) liste les 45 outils tels qu'exposés par le serveur (`tools/list`) : `name`, `title`, `description`, `inputSchema` (JSON Schema) et `annotations` (`readOnlyHint`, `destructiveHint`, etc.).

Exemples : `get_company_pnl`, `get_trial_balance`, `find_unpaid_customer_invoices`, `prepare_rdv_brief`, `generate_fec_export`, `generate_revision_triage`, `generate_charte_ia_cabinet`.

## Se connecter

- **Endpoint MCP** : `https://apps.holco.co/mcp/pennylane/mcp/v1`
- **Authentification** : OAuth 2.0 (Authorization Code + PKCE), Dynamic Client Registration.
- Guides d'installation : [Claude](https://apps.holco.co/mcp/pennylane/install/claude/) · [ChatGPT](https://apps.holco.co/mcp/pennylane/install/chatgpt/) · [Le Chat](https://apps.holco.co/mcp/pennylane/install/mistral/)

## Conformité

- Page produit : https://apps.holco.co/mcp/pennylane/
- Confidentialité : https://apps.holco.co/mcp/pennylane/confidentialite/
- Sécurité et RGPD : https://apps.holco.co/mcp/pennylane/docs/security/
- Conçu pour le secret professionnel comptable (Code pénal art. 226-13) et l'AI Act UE 2024/1689.

## Support

Contact : support via la page produit, ou pierre@holco.co.

---

© HOLCO. PennyPilot et son serveur sont propriétaires. Ce dépôt est publié à des fins de transparence (catalogue d'outils et documentation).
