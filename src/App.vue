<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h1>SpaceX Launches</h1>
      </div>
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main>
        <div class="feature">
      <h2>Timeline des lancements </h2>
      <Timeline url='https://api.spacexdata.com/v3/launches'/>
      </div>
      <div class="feature">
        <h2>Voir le prochain lancement</h2>
        <NextLaunch url='https://api.spacexdata.com/v4/launches/next'/>
      </div>
      <div class="feature">
      <h2>Voir les lancements réussis </h2>
      <LaunchesData url='https://api.spacexdata.com/v3/launches?launch_success=true' />
      </div>
      <div class="feature">
       <h2>Voir les lancements échoués </h2>
      <LaunchesData url='https://api.spacexdata.com/v3/launches?launch_success=false' />
      </div>
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

<style >

#app {
  background-image: url('~@/assets/background.jpg');
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  font-family: 'Roboto', sans-serif;
}

h2 {
  color: white;
}

.v-main__wrap {
  text-align: center;
}

.v-main .feature {
  margin-top: 3em;
  margin-bottom: 3em;
  border: 1px solid white;
  border-radius: 40px;
  width: fit-content;
  margin-left: auto;
  margin-right: auto;
  padding:1.5em
}

</style>
