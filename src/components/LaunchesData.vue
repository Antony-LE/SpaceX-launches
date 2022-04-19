<template>
<section>
         <v-btn v-on:click="updateLaunches(); isHidden= !isHidden" rounded color="primary" dark >
             {{ isHidden ? "Masquer les lancements": "Charger les lancements"}}
        </v-btn>
 <v-container v-if="isHidden===true"  class="grey lighten-5">
    <v-row no-gutters>
      <v-col
        v-for="LaunchData in LaunchesData"
        :key="LaunchData.flight_number"
        cols="12"
        sm="4"
      >
          <v-card class="mx-auto" max-width="400" max-height="900" height="60vh">
      <v-img
        class="white--text align-end"
        max-width="100%"
        max-height="100%"
        v-bind:src="LaunchData.links.mission_patch_small"
      >
      </v-img>
      <v-card-title>Mission : {{ LaunchData.mission_name }}</v-card-title>
      <v-card-subtitle class="pb-0">
        Date : {{ LaunchData.launch_date_utc }}
      </v-card-subtitle>
      <v-card-text class="text--primary">
        <div><strong>Site de lancement :</strong> {{ LaunchData.launch_site.site_name_long }} </div>
        <br>
        <div>{{ LaunchData.details }}</div>
      </v-card-text>
    </v-card>
  </v-col>
    </v-row>
  </v-container>
</section>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LaunchesData',
  props: {
    url: String,
  },
  data() {
    return {
      LaunchesData: {},
      isHidden: false,
    };
  },
  methods: {
    // Requête Axios récupérant les infos du prochain lancement
    updateLaunches() {
      axios
        .get(this.url)
        .then((response) => { this.LaunchesData = response.data; });
    },
  },
};
</script>

<style scoped>
  ul {
          list-style-type: none;
      }

  li {
          margin-bottom: 1em;
          border: solid white 1px;
          width: 30vw;
          margin-left: auto;
          margin-right: auto;
          padding: 1.5em;
      }

    .mx-auto {
        margin-bottom: 5em;
        padding: 2em;
        overflow: auto;
    }

</style>
