# Architecture de spring-ai-secure-rag

[Ouvrir le HTML autonome](architecture.html) · [Spécification Archify](architecture.archify.json)

Télécharger le HTML et l'ouvrir localement dans un navigateur : GitHub affiche son code et ne l'exécute pas. Aucun hébergement supplémentaire n'est nécessaire.

Vue compacte des composants du dépôt au commit `c36476d569267d8bc3855a420a795c5cd7478aa3`. Les flèches représentent les opérations indiquées, pas une preuve de déploiement ni un graphe exhaustif des appels. Les composants secondaires sans flèche complètent l'inventaire ; leurs liens détaillés restent dans les sources ci-dessous.

Identité par en-têtes et index en mémoire : démonstration locale, sans authentification de production ni LLM distant.

Le texte du diagramme est en français. Les commandes fixes du Viewer et l'attribut HTML `lang` restent en anglais, langue de repli d'Archify 2.17. Affichage statique initial, thèmes clair et sombre ; aucune animation activée.

![Aperçu de la carte](architecture-preview.png)

## Sources vérifiées

| Composant | Source au commit de référence |
| --- | --- |
| Identité HTTP | [src/main/java/dev/anvium/securerag/config/TenantIdentityFilter.java:17–25](https://github.com/murillo-consulting/spring-ai-secure-rag/blob/c36476d569267d8bc3855a420a795c5cd7478aa3/src/main/java/dev/anvium/securerag/config/TenantIdentityFilter.java#L17-L25) |
| API RAG | [src/main/java/dev/anvium/securerag/api/RagController.java:16–24](https://github.com/murillo-consulting/spring-ai-secure-rag/blob/c36476d569267d8bc3855a420a795c5cd7478aa3/src/main/java/dev/anvium/securerag/api/RagController.java#L16-L24) |
| SecureRagService | [src/main/java/dev/anvium/securerag/service/SecureRagService.java:65–73](https://github.com/murillo-consulting/spring-ai-secure-rag/blob/c36476d569267d8bc3855a420a795c5cd7478aa3/src/main/java/dev/anvium/securerag/service/SecureRagService.java#L65-L73) |
| SimpleVectorStore | [src/main/java/dev/anvium/securerag/config/RagConfiguration.java:21–23](https://github.com/murillo-consulting/spring-ai-secure-rag/blob/c36476d569267d8bc3855a420a795c5cd7478aa3/src/main/java/dev/anvium/securerag/config/RagConfiguration.java#L21-L23) |
| Réponse citée | [src/main/java/dev/anvium/securerag/service/SecureRagService.java:82–90](https://github.com/murillo-consulting/spring-ai-secure-rag/blob/c36476d569267d8bc3855a420a795c5cd7478aa3/src/main/java/dev/anvium/securerag/service/SecureRagService.java#L82-L90) |
| Embeddings locaux | [src/main/java/dev/anvium/securerag/config/RagConfiguration.java:16–23](https://github.com/murillo-consulting/spring-ai-secure-rag/blob/c36476d569267d8bc3855a420a795c5cd7478aa3/src/main/java/dev/anvium/securerag/config/RagConfiguration.java#L16-L23) |

## Reproduction

Prérequis : Node.js et le skill [Archify](https://github.com/tt-a1i/archify), version 2.17 (MIT). Depuis la racine du dépôt, remplacer `<ARCHIFY>` par le répertoire du skill installé :

```text
rtk node <ARCHIFY>/bin/archify.mjs validate architecture docs/architecture/architecture.archify.json --repo-root . --quality showcase --json
rtk node <ARCHIFY>/bin/archify.mjs deliver architecture docs/architecture/architecture.archify.json docs/architecture/architecture.html --repo-root . --quality showcase --json
rtk node <ARCHIFY>/bin/archify.mjs visual-check docs/architecture/architecture.html --json
```

La révision source doit être présente dans le clone pour vérifier les références. Après une modification du JSON, relancer les trois commandes puis inspecter les captures des deux thèmes. Ne pas éditer le HTML généré.

## Vérifications et limites

Validation et livraison : **9/9 contrôles showcase**, zéro erreur et zéro avertissement. Le reçu portable `acceptance.json` lie les octets exacts aux contrôles et distingue la preuve navigateur de la revue des images.

Les tests applicatifs ne sont pas relancés : seuls le JSON, le HTML, les preuves documentaires et le lien du README changent. Cette documentation n'établit pas la santé d'un service, la sécurité d'une installation ni une conformité réglementaire.

Retour arrière : retirer le lien du README et les cinq fichiers de cette documentation, ou révoquer son commit. Aucun changement applicatif ou déploiement n'est associé.
