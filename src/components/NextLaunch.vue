<template>
     <section class="next-launch">
        <button v-on:click="updateNextLaunch">Charger le lancement</button>
        <p v-if="nextLaunchDatas.name">Le prochain lancement SpaceX de la fusée
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
