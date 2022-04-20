<template>
<section>
<v-btn v-on:click="updateTimeline(); setLoading(); isHidden= !isHidden" rounded color="primary" dark >
             {{ isHidden ? "Masquer l'historique": "Charger la timeline"}}
        </v-btn>
     <v-timeline v-if="isHidden===true">
       <TrinityRingsSpinner 
          v-if="loading" 
          :animation-duration="1200"
          :size="70"
           color="#1976D2"
     />
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
        <v-card-subtitle> Fusée : {{launch.rocket.rocket_name}}</v-card-subtitle>
        <v-card-text> {{launch.details}}</v-card-text>
      </v-card>
    </v-timeline-item>
  </v-timeline>
  </section>
</template>
<script>
import axios from 'axios';
import {TrinityRingsSpinner} from 'epic-spinners'

export default {
  name: 'Timeline',
  props: {
    url: String,
  },
  components: {
    TrinityRingsSpinner
  },
  data() {
    return {
      launches: [],
      isHidden: false,
      loading: true,
    };
  },
  methods: {
    updateTimeline() {
      axios
        .get(this.url)
        .then((response) => { this.launches = response.data });
    },

    setLoading() {
      axios
        .get(this.url)
        .then(() => { this.loading = false })
        .catch(error => error.response.data);
    },

  },
};
</script>

<style scoped>

      span {
        font-size: 3em;
        font-weight: lighter;
        color: white;
      }

      h1 {
          text-align: center;
          font-size: 4em;
      }

      img {
          height: 100px;
          width: 100px;
      }

      .v-timeline {
          width: 70vw;
      }

      .trinity-rings-spinner {
        margin-top: 1em;
        margin-bottom: 1em;
        margin-left: auto;
        margin-right: auto;
        text-align: center;
      }

</style>
