<template>
  <v-container>
    
      <div>
        <!-- <img :src="movieImage" width="100" height="200" @click="getDetails(id)"> -->
    </div>
  </v-container>

</template>

<script>
  export default {
    name: 'HelloWorld',
    props:["movieImage", "nameMovie", "getDetails", "id"],

    data(){
        return {
            
        }
    }
    }
</script>
