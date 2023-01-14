# freeapi

## APi Sirene V3

Intégration rapide de l'API Sirene. Pour l'utiliser il faut avoir une application enregistrée.
https://api.insee.fr/catalogue/

Documentation : https://www.sirene.fr/static-resources/htm/sommaire.html

### Installation

```
    composer require jeromeklam/freeapi
```

Il faut donc un compte et une pplication enregistrée.
Les jetons générés sont stockés sur disque et ont une durée de validité jusqu'à minuit de la journée en cours.

La limite des appels est documentée ici : https://api.gouv.fr/guides/quelle-api-sirene

### Exemples d'utilisation

```
    $api_cfg = [
        'key'    => '<customer key>',
        'secret' => '<customer secret>',
        'path'   => '<token store path>' 
    ];
    $api     = \FreeAPI\INSEE\Sirene\Siret::getInstance($api_cfg);
    $result  = $api->find(['nom' => '*zoo*', 'ville' => 'amneville']);
    foreach ($result as $unEtablissement) {
        ...
    }
```

Les éléments pour la recheche sont :

* Pour les appels siren :
  * siren
  * nom
* Pour les appels siret :
  * siren
  * siret
  * nom
  * cp
  * ville
  * sigle

Il est possible de rechercher avec les caractères suivants :

* "*zoo" pour se termine par zoo
* "zoo*" pour commence par zoo
* "*zoo*" pour contient zoo
* "zoo~" pour ressemble à zoo, (une explication détaillée ici : https://fr.wikipedia.org/wiki/Distance_de_Levenshtein)
