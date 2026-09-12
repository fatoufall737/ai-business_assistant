# ai-business_assistant

## Partie 1 – Anatomie d'un prompt

### Objectif

Construire un prompt permettant d'analyser les retours clients d'une entreprise, en identifiant clairement les composantes qui le structurent.

### Prompt utilisé

Tu es un analyste customer experience spécialisé dans l'analyse de retours clients.

Voici un ensemble de retours clients laissés par des utilisateurs de l'application Yassir :

"Très mauvaise expérience. J'ai confirmé ma commande par app, puis le livreur m'a appelé pour confirmer à nouveau. Après 45 minutes d'attente, on m'informe que la commande est annulée car le restaurant a augmenté ses prix. On me demande simplement de passer une autre commande. Service très décevant, je ne recommande absolument pas cette application."
"j'adore cette application pour acheter des trucs le problème c'est que ça prend un peu trop de temps donc il faut commander à l'avance. c'est vraiment très pratique donc je l'adore mais je pense à prendre un peu trop de temps mais merci"
"J'ai essayé d'utiliser cette app de livraison pendant 2 semaines, mais mon expérience a été très décevante. La majorité de mes commandes comportaient des erreurs, les livreurs mettent énormément de temps à livrer malgré l'erreur, vous ne bénéficiez d'aucun remboursement. Je déconseille donc fortement cette app."
"C'est une super appli, mais les prix des courses sont un peu élevés. J'espère qu'ils les baisseront. La livraison est également chère ; j'espère qu'ils baisseront les prix."
"Franchement, je préfère largement l'ancienne version. La nouvelle mise à jour est beaucoup trop lente et l'expérience est moins fluide. J'espère que les prochaines mises à jour amélioreront les performances."
"L'application est super, mais certains chauffeurs demandent d'annuler la course et d'autres demandent d'ajouter un montant en plus du montant de la commission."

Analyse ces retours et identifie : le sentiment général, les problèmes les plus fréquemment mentionnés, et des recommandations d'amélioration.

Contraintes : n'invente aucune information absente des retours. Reste factuel. Si un retour est ambigu, ne le classe pas arbitrairement.

Réponds uniquement en JSON avec les champs suivants :
{
"sentiment_general": "...",
"problemes_recurrents": ["...", "..."],
"recommandations": ["...", "..."]
}

### Annotation – composantes du prompt

| Composante           | Contenu dans le prompt                                                                                                                           | Rôle                                                                |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| **Rôle**             | "Tu es un analyste customer experience spécialisé dans l'analyse de retours clients."                                                            | Cadre l'identité et le niveau d'expertise attendu du modèle         |
| **Contexte**         | Les 6 avis clients réels de l'application Yassir                                                                                                 | Fournit la matière première à analyser                              |
| **Tâche**            | "Analyse ces retours et identifie : le sentiment général, les problèmes les plus fréquemment mentionnés, et des recommandations d'amélioration." | Définit précisément ce qui est attendu                              |
| **Contraintes**      | "N'invente aucune information absente des retours. Reste factuel. Si un retour est ambigu, ne le classe pas arbitrairement."                     | Limite les hallucinations et impose la prudence sur les cas ambigus |
| **Format de sortie** | JSON avec 3 champs nommés (`sentiment_general`, `problemes_recurrents`, `recommandations`)                                                       | Rend la réponse exploitable directement par une application         |

### Réponse obtenue

```json
{
  "sentiment_general": "Mitigé à négatif : plusieurs retours très négatifs (annulations, erreurs de commande, absence de remboursement, prix élevés), un retour neutre à positif sur la praticité malgré la lenteur, et un retour mitigé satisfait du service mais critique sur les pratiques de certains chauffeurs.",
  "problemes_recurrents": [
    "Annulations de commandes après confirmation, notamment liées à des changements de prix côté restaurant",
    "Délais de livraison longs / lenteur perçue de l'application",
    "Erreurs fréquentes dans les commandes sans remboursement associé",
    "Prix jugés élevés, à la fois pour les courses et la livraison",
    "Dégradation des performances après une mise à jour, expérience moins fluide qu'avant",
    "Comportements problématiques de certains chauffeurs : demandes d'annulation de course ou de suppléments"
  ],
  "recommandations": [
    "Mettre en place une politique de remboursement ou de compensation claire en cas d'erreur",
    "Améliorer la synchronisation des prix en temps réel avec les restaurants partenaires",
    "Investiguer et réduire les délais de livraison, notamment en optimisant l'affectation des livreurs",
    "Revoir la stabilité et la fluidité de l'application suite aux mises à jour récentes"
  ]
}
```

### Capture d'écran

![Réponse Partie 1](./partie1_reponse.png)

### Remarque

Deux avis étaient explicitement mixtes (ex. un avis satisfait du service de trajets mais critique sur la livraison). Conformément à la contrainte donnée, ils n'ont pas été forcés dans une catégorie unique.
