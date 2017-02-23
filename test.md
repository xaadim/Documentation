## Openlayers offlineMap Service

Service pour créer une carte hors ligne dans Openlayers v3.xx v4.X en se basant sur les couches cachées de Geoserver en local.

## Installation : 

- Attacher le fichier offlineMapService.js dans votre projet. 
- Ajouter le module 'offlineTilesModule' dans votre projet  angular. 

## Utilisation : 
 
```javascript
// Ajout de la couche 
offlineTilesService.createOffLineTiles(gridSetParams, layerParams, map);
```
### gridSetParams : paramètres de la grille de projection récupérée depuis Geoserver

exemple : 
 ```javascript
var gridSetParams = {
    name : 'EPSG:27572_sdis17_2000',
    extent : [225000, 1910000, 533000, 2240000],
    resolutions : [209.99999999999997, 140 ,70 , 27.999999999999996,
    13.999999999999998, 6.999999999999999, 5.6, 4.199999999999999, 2.8, 1.4, 0.5599999999999999, 0.27999999999999997],
    projection : 'EPSG:27572',
    tileHeight : 2000,
    tileWidth  : 2000
  };	
```


### layerParams : paramètres de la couche

exemple : 
```javascript
var layerParams ={
    baseUrl : 'offlineTiles', // dossier de base des images cachées
    layerName :'sdis17_vecteur_complet',  // nom de la couche 
    extension : 'png', // extension des images cachées {si pas définie, png est choisie par défaul}
    projection : gridSetParams.projection, // Projection des images 
};
```

### map : la carte Openlayers
