<template>
  <div id="app">
      
    <v-row class="text-center ">
      <v-col>
        <h1 class="font-weight-bold" style="text-align: center; color: #0B488C ">
          The Moviez Review
        </h1>
      </v-col>
    </v-row>


      <div id="nav" style="text-align: center; margin-top: 20px; background-color: #0B488C; height: 5vh; font-size: 35px; ">
            <router-link to="/" style="margin-right: 30px; color: white; ">Tous les films</router-link>
            <router-link to="/liste" style="margin-right: 30px; color: white;">Ma liste</router-link>
      </div>
      

      <router-view/>
  </div>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
