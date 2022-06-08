<script>
    // import 'leaflet/dist/leaflet.css';
    import {LeafletMap} from '../services/LeafletMap';
    import {getContext, onMount} from "svelte";
  
    const placemarkService = getContext("PlacemarkService");
    
    export let latitude;
    export let longitude;

    const mapConfig = {
      location: {lat: latitude, lng: longitude},
      zoom: 20,
      minZoom: 1,
    };
    let map = null;
  
    onMount(async () => {
      map = new LeafletMap("LeafletMap", mapConfig);
      map.showZoomControl();
      map.showLayerControl();
      map.addMarker({lat: latitude, lng: longitude});
    });
  </script>
  
  <div class="box" id="LeafletMap" style="height:400px">
  </div>