<template>
   
  <div class="container">
      
    <div class="row">
        
      <div class="">
          
        <h1>Leaftlet & Vue</h1>
        
        <hr>

        <app-basic-map-one></app-basic-map-one>
                  
      </div>
        
    </div>
      
  </div>
    
</template>

<script>
    
  import BasicMapOne from "./components/BasicMapOne.vue";
  export default {
      
    components: {
        
      appBasicMapOne: BasicMapOne
        
    },

  }
    
</script>