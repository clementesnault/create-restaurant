<template>
  <v-app>
    <HomeBar/>
      <v-main>
        <router-view/>
      </v-main>
  </v-app>
</template>

<script>
import HomeBar from './components/HomeBar.vue';

export default {
  name: 'App',

  data: () => ({
    //
  }),

  components: {
    HomeBar,
  },
}
</script>
