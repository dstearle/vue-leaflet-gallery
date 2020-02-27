<template>

  <div class="card">

    <h5 class="card-header bg-light">Custom Icons</h5>

    <div class="card-body p-5">

      <div style="height: 500px; width: 100%">

        <!-- Icon Controls -->
        <div style="height: 20%; overflow: auto;">

            <h6>Icon Settings</h6>

            <label for="iconSize">Icon size:</label>

            <input
                id="iconSize"
                v-model="iconSize"
                type="range"
                min="1"
                max="200"
                value="64"
            >

            <label for="customTextInput">Custom text: </label>

            <input
                id="customTextInput"
                v-model="customText"
                type="text"
            >

        </div>

        <!-- Leaflet Map -->
        <l-map
          :zoom="zoom"
          :center="center"
          style="height: 80%"
        >

            <!-- Tile Layer -->
            <l-tile-layer
                :url="url"
                :attribution="attribution"
            />

            <!-- Default Icon -->
            <l-marker :lat-lng="[37.52732, -119.278882]" />

            <!-- Create image icon (icon) from l-icon tag -->
            <!-- <l-marker :lat-lng="[37.52732, -119.278882]">
                <l-icon
                    :icon-size="dynamicSize"
                    :icon-anchor="dynamicAnchor"
                    icon-url="./../images/dinoIcon.png"
                />
            </l-marker> -->

            <!-- Use icon given in icon property -->
            <l-marker
                :lat-lng="[32.680863, -117.185148]"
                :icon="icon"
            />

        </l-map>

      </div>

    </div>

  </div>

</template>

<script>

  import { LMap, LTileLayer, LMarker, } from "vue2-leaflet";
  import { latLng, icon } from "leaflet";

  export default {

    name: "Icon",

    components: {

        LMap,
        LTileLayer,
        LMarker,
        // LIcon

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
        // Icon Properties
        icon: icon({
            iconUrl:  require("./../images/dinoIcon.png"),
            iconSize: [40, 40],
            iconAnchor: [16, 37]
        }),
        staticAnchor: [16, 37],
        customText: "Foobar",
        iconSize: 64

      };

    },

    computed: {

        dynamicSize() {

        return [this.iconSize, this.iconSize * 1.15];

        },

        dynamicAnchor() {

        return [this.iconSize / 2, this.iconSize * 1.15];

        }

    },

    methods: {

      zoomUpdate(zoom) {
        this.currentZoom = zoom;
      },

      centerUpdate(center) {
        this.currentCenter = center;
      },

    }

  };

</script>

<style>

    .someExtraClass {

        background-color: aqua;
        padding: 10px;
        border: 1px solid #333;
        border-radius: 0 20px 20px 20px;
        box-shadow: 5px 3px 10px rgba(0, 0, 0, 0.2);
        text-align: center;
        width: auto !important;
        height: auto !important;
        margin: 0 !important;

    }

</style>