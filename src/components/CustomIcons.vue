<template>

  <div class="card">

    <h5 class="card-header bg-light">Custom Icons</h5>

    <div class="card-body p-5">

      <div style="height: 500px; width: 100%">

        <!-- Leaflet Map -->
        <l-map
          v-if="showMap"
          :zoom="zoom"
          :center="center"
          :options="mapOptions"
          style="height: 80%"
          @update:center="centerUpdate"
          @update:zoom="zoomUpdate"
        >
          <l-tile-layer
            :url="url"
            :attribution="attribution"
          />

        </l-map>

      </div>

    </div>

  </div>

</template>

<script>

  import { latLng } from "leaflet";
  import { LMap, LTileLayer, } from "vue2-leaflet";

  export default {

    name: "Example",

    components: {
      LMap,
      LTileLayer,
    },

    data() {

      return {

        // Zoom out
        zoom: 5,
        // Map location
        center: latLng(37.52732, -119.278882),
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        attribution:
          '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
        // Popup location
        withPopup: latLng(37.52732, -119.278882),
        // Tooltip location
        withTooltip: latLng(32.68338, -117.184274),
        currentZoom: 11.5,
        currentCenter: latLng(37.52732, -119.278882),
        showParagraph: false,
        mapOptions: {
          zoomSnap: 0.5
        },
        showMap: true

      };

    },

    methods: {

      zoomUpdate(zoom) {
        this.currentZoom = zoom;
      },
      centerUpdate(center) {
        this.currentCenter = center;
      },
      showLongText() {
        this.showParagraph = !this.showParagraph;
      },
      innerClick() {
        alert("Click!");
      }

    }

  };

</script>