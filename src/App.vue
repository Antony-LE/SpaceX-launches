<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h2>SpaceX Launches</h2>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <h2>Voir le prochain lancement</h2>
    <NextLaunch url='https://api.spacexdata.com/v4/launches/next' />
    <hr>
      <h2>Voir les lancements réussis </h2>
      <LaunchesData url='https://api.spacexdata.com/v3/launches?launch_success=true' />
       <hr>
       <h2>Voir les lancements échoués </h2>
      <LaunchesData url='https://api.spacexdata.com/v3/launches?launch_success=false' />
       <hr>
      <h2>Historique des lancements </h2>
      <Timeline url='https://api.spacexdata.com/v3/launches'/>
    </v-main>
  </v-app>
</template>

<script>
import NextLaunch from './components/NextLaunch.vue'
import LaunchesData from './components/LaunchesData.vue'
import Timeline from './components/Timeline.vue';

export default {
  name: 'App',

  components: {
    NextLaunch, LaunchesData,
    Timeline,
  },
};
</script>
