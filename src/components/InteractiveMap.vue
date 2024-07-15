  <template>
    <div id="map"></div>
  </template>
  
  <script>
  import { onMounted } from 'vue';
  import L from 'leaflet';
  import 'leaflet/dist/leaflet.css';
  import geojsonData from '../datas/Data_geojson_compliant.json';
  
  export default {
    name: 'InteractiveMap',
    setup() {
      onMounted(() => {
        const map = L.map('map').setView([45.4397, 4.3872], 12.6);
  
        L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
          maxZoom: 19,
          attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
        }).addTo(map);
  
        console.log(geojsonData);  // Vérifiez que les données GeoJSON sont chargées
  
        L.geoJSON(geojsonData, {
          pointToLayer: function (feature, latlng) {
            // Créez un marqueur pour chaque point
            return L.marker(latlng);
          },
          onEachFeature: function (feature, layer) {
            // Ajoutez une popup si la propriété popupContent existe
            if (feature.properties && feature.properties.popupContent) {
              layer.bindPopup(feature.properties.popupContent);
            }
          }
        }).addTo(map);
      });
    }
  };
  </script>
  
  <style>
  #map {
    width: 100%;
    height: 500px;
    border: solid #3FA73C;
    border-radius: 0.5em;
  }
  </style>
  