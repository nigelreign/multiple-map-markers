##View multiple markers in a map

#using javascript or typescript

![mapppp](https://user-images.githubusercontent.com/37867005/93746135-ecb37f80-fbf4-11ea-91fe-7b2262f22a2f.JPG)


If you want to use it in an angular, ionic app do the following steps

1. In your app.ts 

    ```declare const google;```
    
    or import
    
    ```import { google } from 'google-maps';```

2. If you want the app to load on the first page using angular use

    ``` ionViewDidEnter() {
           this.openMapView();
         } 
         
3. then in your openMapView method put:

    ``` var locations = [
             ['Bondi Beach', -33.890542, 151.274856, 10],
             ['Coogee Beach', -33.923036, 151.259052, 5],
             ['Cronulla Beach', -34.028249, 151.157507, 3],
             ['Manly Beach', -33.80010128657071, 151.28747820854187, 2],
             ['Maroubra Beach', -33.950198, 151.259302, 1]
           ];
       
           var map = new google.maps.Map(document.getElementById('map'), {
             zoom: 10,
             center: new google.maps.LatLng(-33.92, 151.25),
             mapTypeId: google.maps.MapTypeId.ROADMAP
           });
       
           var infowindow = new google.maps.InfoWindow();
       
           var marker, i;
       
           for (i = 0; i < locations.length; i++) {
             marker = new google.maps.Marker({
               position: new google.maps.LatLng(locations[i][1], locations[i][2]),
               map: map
             });
       
             google.maps.event.addListener(marker, 'click', (function (marker, i) {
               return function () {
                 infowindow.setContent(locations[i][0]);
                 infowindow.open(map, marker);
               }
             })(marker, i));
       
       
             console.log('show map')
           }```
           
 4. In your template.html dont put the following line 
    
        ```<div id="map"></div>```
   
  inside an ngIf* statement or you will get an error
  
  ```Error: Uncaught (in promise): ReferenceError: google is not defined```

