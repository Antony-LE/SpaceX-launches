<template>
<section>
         <v-btn v-on:click="updateLaunches(); isHidden= !isHidden" rounded color="primary" dark >
             {{ isHidden ? "Masquer les lancements": "Charger les lancements"}}
        </v-btn>
        <ul v-if="isHidden==true">
            <li v-for="LaunchData in LaunchesData" v-bind:key="LaunchData.flight_number">
                <p>Nom : {{ LaunchData.mission_name }}</p>
                <p>Date de lancement : {{ LaunchData.launch_date_utc }}</p>
                <p>Détails de la mission : {{ LaunchData.details }}</p>
                <img v-bind:src= 'LaunchData.links.mission_patch_small' alt='mission-patch'>
                <p>Article de presse :
                    <a v-bind:href="LaunchData.links.article_link"> Voir l'article</a>
                </p>
                <p>Lien Youtube : <a v-bind:href="LaunchData.links.video_link"> Voir la vidéo</a></p>
            </li>
        </ul>
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

</style>
