## Openlayers offlineMap Service

Service pour créer une carte hors ligne dans Openlayers v4.6.4 ou plus en se basant sur les couches cachées de Geowebcache via GeoServer 2.12.x.

## OPENLAYERS
Ce service nécessite une installation de Openlayers v4.6.4 ou plus. Merci de vérifier la version de Openlayers dans votre projet. 

## INSTALLATION: 

- Attacher le fichier offlineMapService.js dans votre projet. 
```html 
    <script src="offlineTilesService.js" type="text/javascript"></script>
 ```
- Ajouter le module 'offlineTilesModule' dans votre projet. 
```javascript
    myApp.controller('myCtrl', function ($scope, offlineTilesService){});
```
## PARAMETRES:
### gridSetParams: paramètres de la grille de projection récupérée depuis Geoserver

exemple : 
 ```javascript
    var gridSetParams = {
        name : 'EPSG_27572_sdis17_mobile',
        extent : [225000, 1910000, 533000, 2240000],
        resolutions : [210, 140, 70, 28, 14, 7, 5.6, 4.2, 2.8, 1.4, 0.56, 0.28],
        projection : 'EPSG:27572',
        tileHeight : 1024,
        tileWidth  : 1024
    };	
```

### layerParams: paramètres de la couche

exemple : 
```javascript
    var layerParams = {
        baseUrl : 'offlineTiles', // dossier de base des images cachées
        layerName :'sdis17_vecteur_complet'  // nom de la couche
    };
```

## UTILISATION: 
 
```javascript
    //création d'une couche offline de type image (png)
    var imageTile  = offlineTilesService.createOffLineTilesImage(gridSetParams, layerParams);
    map.addLayer(imageTile);
```

```javascript
    //création d'une couche offline de type image (png)
    var vectorTile = offlineTilesService.createOffLineTilesVector(gridSetParams, layerParams);
    map.addLayer(vectorTile);
```
