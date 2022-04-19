<template>
<section>
<v-btn v-on:click="updateTimeline(); isHidden= !isHidden" rounded color="primary" dark >
             {{ isHidden ? "Masquer l'historique": "Charger l'historique"}}
        </v-btn>
     <v-timeline v-if="isHidden==true">
    <v-timeline-item
     v-for="launch in launches" v-bind:key="launch.flight_number"
      large
    >
      <template v-slot:icon>
        <v-avatar>
          <img v-bind:src="launch.links.mission_patch_small">
        </v-avatar>
      </template>
      <template v-slot:opposite>
        <span>{{ launch.launch_year }}</span>
      </template>
      <v-card class="elevation-2">
        <v-card-title class="text-h5"> Mission : {{launch.mission_name}}</v-card-title>
        <v-card-subtitle> Rocket : {{launch.rocket.rocket_name}}</v-card-subtitle>
        <v-card-text> {{launch.details}}</v-card-text>
      </v-card>
    </v-timeline-item>
  </v-timeline>
  </section>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Timeline',
  props: {
    url: String,
  },
  data() {
    return {
      launches: [],
      isHidden: false,
    };
  },
  methods: {
    updateTimeline() {
      axios
        .get(this.url)
        .then((response) => { this.launches = response.data });
    },

  },
};
</script>

<style scoped>
 header {
          background-color: white;
          color: #004F87;
          margin: 1em;
          padding-top: 2em;
          padding-bottom: 2em;
      }

      span {
        font-size: 1.7em;
        font-weight: lighter;
      }

      h1 {
          text-align: center;
          font-size: 4em;
      }
</style>
