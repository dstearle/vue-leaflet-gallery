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
          <l-marker :lat-lng="[32.924717, -118.491696]">

            <l-icon
              :icon-size="dynamicSize"
              :icon-anchor="dynamicAnchor"
              :icon-url= myIcon
            />
            
          </l-marker>

          <!-- Use icon given in icon property -->
          <l-marker
            :lat-lng="[32.680863, -117.185148]"
            :icon="icon"
          />

          <!-- Create HTML icon (divIcon) by providing content inside the l-icon tag -->
          <l-marker :lat-lng="[33.098172, -116.993914]">

            <l-icon
              :icon-anchor="staticAnchor"
              class-name="someExtraClass"
            >

              <div class="headline">{{ customText }}</div>

              <img :src= myIcon style="width: 5rem; height: 5rem">

            </l-icon>

          </l-marker>

          <!-- Another custom HTML Icon -->
          <l-marker :lat-lng="[33.143976, -117.336785]">

            <l-icon
              :icon-anchor="staticAnchor"
              class-name="custom-div-icon"
            >

              <div style='background-color:#c30b82;' class='marker-pin'></div>
              
              <img :src= myIcon class="my-auto">

            </l-icon>

          </l-marker>

        </l-map>

      </div>

    </div>

  </div>

</template>

<script>

  import { LMap, LTileLayer, LMarker, LIcon } from "vue2-leaflet";
  import { latLng, icon } from "leaflet";

  export default {

    name: "Icon",

    components: {

      LMap,
      LTileLayer,
      LMarker,
      LIcon

    },

    data() {

      return {

        myIcon: require("./../images/dinoIcon.png"),

        // Zoom out
        zoom: 5,
        // Map location
        center: latLng(37.52732, -119.278882),
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        attribution:
          '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
        // Icon Properties
        icon: icon({
          iconUrl: require("./../images/dinoIcon.png"),
          iconSize: [40, 40],
          iconAnchor: [16, 37]
        }),
        staticAnchor: [16, 37],
        customText: "Brachiosaurus",
        iconSize: 64

      };

    },

    computed: {

      // For resizing icon dynamically
      dynamicSize() {

      return [this.iconSize, this.iconSize * 1.15];

      },

      // Adjust anchor position when icon size changes
      dynamicAnchor() {

      return [this.iconSize / 2, this.iconSize * 1.15];

      }

    },

  };

</script>

<style>

  .someExtraClass {

    background-color: lightgreen;
    padding: 10px;
    border: 1px solid #333;
    border-radius: 0 20px 20px 20px;
    box-shadow: 5px 3px 10px rgba(0, 0, 0, 0.2);
    text-align: center;
    width: auto !important;
    height: auto !important;
    margin: 0 !important;

  }

  .marker-pin {

    width: 40px;
    height: 40px;
    border-radius: 50% 50% 50% 0;
    background: #c30b82;
    position: absolute;
    transform: rotate(-45deg);
    left: 50%;
    top: 50%;
    margin: -15px 0 0 -15px;

  }

.marker-pin::after {

  content: '';
  width: 34px;
  height: 34px;
  margin: 3px 0 0 3px;
  background: #fff;
  position: absolute;
  border-radius: 50%;

 }

.custom-div-icon img {

  position: absolute;
  width: 24px;
  font-size: 22px;
  left: 0;
  right: 0;
  margin: 10px auto;
  text-align: center;

}

</style>