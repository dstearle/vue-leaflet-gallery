<template>

  <div class="card">

    <h5 class="card-header bg-light">Basic Map</h5>

    <div class="card-body p-5">

      <div style="height: 500px; width: 100%">

        <!-- Toggle Buttons -->
        <div style="height: 200px overflow: auto;">

          <p>First marker is placed at {{ withPopup.lat }}, {{ withPopup.lng }}</p>

          <p>Center is at {{ currentCenter }} and the zoom is: {{ currentZoom }}</p>

          <button @click="showLongText">

            Toggle long popup

          </button>

          <button @click="showMap = !showMap">

            Toggle map
            
          </button>

        </div>

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

          <!-- Popup -->
          <l-marker :lat-lng="withPopup">
            <l-popup>
              <div @click="innerClick">
                I am a popup
                <p v-show="showParagraph">
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
                  sed pretium nisl, ut sagittis sapien. Sed vel sollicitudin nisi.
                  Donec finibus semper metus id malesuada.
                </p>
              </div>
            </l-popup>
          </l-marker>

          <!-- Tooltip -->
          <l-marker :lat-lng="withTooltip">
            <l-tooltip :options="{ permanent: true, interactive: true }">
              <div @click="innerClick">
                I am a tooltip
                <p v-show="showParagraph">
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
                  sed pretium nisl, ut sagittis sapien. Sed vel sollicitudin nisi.
                  Donec finibus semper metus id malesuada.
                </p>
              </div>
            </l-tooltip>
          </l-marker>

        </l-map>

      </div>

    </div>

  </div>

</template>

<script>

  import { latLng } from "leaflet";
  import { LMap, LTileLayer, LMarker, LPopup, LTooltip } from "vue2-leaflet";

  export default {

    name: "Example",

    components: {
      LMap,
      LTileLayer,
      LMarker,
      LPopup,
      LTooltip
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
