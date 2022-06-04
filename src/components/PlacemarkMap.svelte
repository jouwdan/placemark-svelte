<script>
    import 'leaflet/dist/leaflet.css';
    import {LeafletMap} from '../services/LeafletMap';
    import {getContext, onMount} from "svelte";
  
    const placemarkService = getContext("PlacemarkService");
    let restaurantsList = [];

    const mapConfig = {
      location: {lat: 52.160858, lng: -7.152420},
      zoom: 8,
      minZoom: 1,
    };
    let map = null;
  
    onMount(async () => {
      map = new LeafletMap("LeafletMap", mapConfig);
      map.showZoomControl();
      map.showLayerControl();

      restaurantsList = await placemarkService.getRestaurants();
      restaurantsList.forEach(restaurant => {
          addPlacemark(restaurant);
      });
    });

    function addPlacemark(restaurant) {
    const restaurantStr = `${restaurant.name}`;
    map.addMarker({lat: restaurant.latitude, lng: restaurant.longitude}, restaurantStr);
  }
  </script>
  
  <div class="box" id="LeafletMap" style="height:800px">
  </div>