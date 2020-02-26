<template>
   
  <div class="container">
      
    <div class="row">
        
      <div class="">
          
        <h1>Leaftlet & Vue</h1>
        
        <hr>

        <app-basic-map-one></app-basic-map-one>

        <br>

        <app-custom-icons></app-custom-icons>
                  
      </div>
        
    </div>
      
  </div>
    
</template>

<script>
    
  import BasicMapOne from "./components/BasicMapOne.vue";
  import CustomIcons from "./components/CustomIcons.vue";

  export default {
      
    components: {
        
      appBasicMapOne: BasicMapOne,

      appCustomIcons: CustomIcons
        
    },

  }
    
</script>