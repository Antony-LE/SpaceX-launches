<template>
     <section class="next-launch">
         <v-btn v-on:click="updateNextLaunch(); isHidden= !isHidden" rounded color="primary" dark >
             {{ isHidden ? "Masquer le lancement": "Charger le lancement"}}
        </v-btn>
        <p v-if="isHidden===true">Le prochain lancement SpaceX de la fusée
          <strong>{{ nextLaunchDatas.name }} </strong> aura lieu le
          <strong>{{ nextLaunchDatas.date_utc }} </strong>
        </p>
    </section>
</template>

<script>
import axios from 'axios';

export default {
  name: 'NextLaunch',
  props: {
    url: String,
  },
  data() {
    return {
      nextLaunchDatas: [],
      isHidden: false,
    };
  },
  methods: {
    // Requête Axios récupérant les infos du prochain lancement
    updateNextLaunch() {
      axios
        .get(this.url)
        .then((response) => { this.nextLaunchDatas = response.data; });
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
