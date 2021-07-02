<template>
<div class="mapleaf">
  <div class="container">
      <div :id="getMapID"></div>
  </div>

<!--  <div class="container">-->
<!--      <div id="mapContainer"></div>-->
<!--  </div>-->
</div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
  name: "MapLeaf",
  data(){
    return {
      center: [33.4484, -112.0740]
    }
  },
  props: {
    id_map: Number
  },

  methods: {
    setupLeafletMap: function () {
      const mapDiv = L.map(this.getMapID).setView(this.center, 10);
      L.tileLayer(
          "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
          {
            attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            maxZoom: 18,
            id: "mapbox/streets-v11",
            accessToken:'pk.eyJ1IjoiYmlyZHJhZGFyMTIzIiwiYSI6ImNrcWFmNHkzbzBtOG4yd2pveHRkcGVhengifQ.SP8H5j4_cDYu1MkPp8aIvQ',
          }
      ).addTo(mapDiv);

      delete L.Icon.Default.prototype._getIconUrl;

      L.Icon.Default.mergeOptions({
        iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
        iconUrl: require('leaflet/dist/images/marker-icon.png'),
        shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
      });

      L.marker(this.center).addTo(mapDiv)
          .bindPopup('A pretty CSS3 popup.<br> Easily customizable.')
          // .openPopup();

    },
  },
  computed: {
    getMapID(){
      return "mapContainer" + this.id_map
    }
  },
  mounted() {
    this.setupLeafletMap();
  },

};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#mapContainer {
  margin: auto;
  width: 50%;
  height: 50vh;
}

#mapContainer1 {
  margin: auto;
  width: 100%;
  height: 50vh;
}

#mapContainer2 {
  margin: auto;
  width: 100%;
  height: 50vh;
}

#mapContainer3 {
  margin: auto;
  width: 100%;
  height: 50vh;
}

</style>
