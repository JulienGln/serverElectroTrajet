# serverElectroTrajet
## Galerne Julien
 Serveur proxy pour l'application electro trajet. Le serveur est écrit en JavaScript avec Express.js

 Il est déployé dans le cloud à l'adresse suivante :
 https://electro-trajet-server.azurewebsites.net/

 ## Routes API

 ### GET /

Redirige vers l'application [client React](https://orange-island-082d39903.4.azurestaticapps.net).

### POST /soap-proxy

Envoie une requête SOAP à https://soap-electro-trajet.vercel.app/ avec les paramètres de distance, autonomie, vitesse moyenne, et temps de chargement. Renvoie le temps de trajet calculé.

**Paramètres de requête :** `distance`, `autonomie`, `vitesse_moyenne`, `tps_chargement`

**Réponse :** Un objet JSON contenant l'information du temps de trajet en heures.

Exemple de réponse :
```json
{ 
  "temps_trajet": 21.56 
}
```

### GET /vehicle-list

Récupère la liste des véhicules à partir de l'[API GraphQL](https://api.chargetrip.io/graphql).

**Paramètres de requête :** Aucun

**Réponse :** Un tableau d'objets JSON, chaque objet représentant un véhicule.

Exemple de réponse :
```json
[
  {
    "id": "1",
    "naming": {
      "make": "Tesla",
      "model": "Model S",
      "chargetrip_version": "2023"
    },
    "media": {
      "image": {
        "thumbnail_url": "https://example.com/image.jpg"
      }
    },
    "battery": {
      "usable_kwh": 100
    },
    "range": {
      "chargetrip_range": {
        "best": 500,
        "worst": 400
      }
    }
  },
  ...
]
```

### GET /proxy

Récupère les bornes près d'un point spécifié, dans un rayon spécifié, par les paramètres de latitude, longitude et rayon. Cette route n'est actuellement pas utilisée.

**Paramètres de requête :** `lat`, `lon`, `radius`

**Réponse :** Un tableau d'objets JSON, chaque objet représentant une borne de recharge.
