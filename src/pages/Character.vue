<template>
  <q-page class="container-sm">
    <div class="row container-sm">
      <h3>{{ name }}</h3>
    </div>
    <div class="row">
      <div class="col-3">
        <img :src="image" :alt="name">
      </div>
      <div class="col data-character-container">
        <div><span class="text-weight-bolder">Status: </span>{{ status }}</div>
        <div><span class="text-weight-bolder">Gender: </span>{{ gender }}</div>
        <div><span class="text-weight-bolder">Origin: </span>{{ originName }}</div>
        <div><span class="text-weight-bolder">Species: </span>{{ species }}</div>
      </div>
    </div>
    <div class="row">
      <h5>Episodios donde apareció</h5>
    </div>
    <div class="row wrap">
      <episode-card 
        :urlEpisode="episode" 
        v-for="(episode, index) in episodes"
        :key="index"
        class="q-mr-sm q-mb-sm"
      />
    </div>
    <div class="row">
      <h5>Personajes interesantes</h5>
    </div>
    <div class="row">
      <character-card 
        v-for="(character, index) in characters" 
        :key="index"
        :characterData="character"
      />
    </div>
  </q-page>
</template>

<script>
// import { defineComponent } from 'vue';
import { api } from 'boot/axios';

import episodeCard from '../components/episodeCard.vue';
import characterCard from '../components/characterCard.vue';

export default {
  name: 'Character',
  components: {
    episodeCard,
    characterCard
  },
  data() {
    return {
      characterData: null,
      idCharacter: null,
      name: null,
      status: null,
      gender: null,
      originName: null,
      species: null,
      image: null,
      episodes: [],
      characters: []
    }
  },
  mounted() {
    this.idCharacter = this.$router.currentRoute.value.params.id;
    this.getCharacter(this.idCharacter);
    this.getInterestingCharacters();
  },
  methods: {
    getCharacter(id) {
      api.get(`/character/${id}`)
        .then(response => {
          this.characterData = response.data;
          this.name = response.data.name;
          this.status = response.data.status;
          this.gender = response.data.gender;
          this.originName = response.data.origin.name;
          this.species = response.data.species;
          this.image = response.data.image;
          this.episodes = response.data.episode;
        })
        .catch(err => {
          console.log(err)
        });
    },
    getInterestingCharacters() {
      let randomNumbers = this.randomNum();

      api.get(`https://rickandmortyapi.com/api/character/${randomNumbers}`)
        .then(response => {
          console.log('response', response)
          this.characters = response.data;
        })
        .catch(err => {
          console.log(err);
        });
    },
    randomNum() {
      var numberList = []; 
      for(var i=0; i < 3; i++){ 
        numberList.push(Math.floor(Math.random() * 100) + 1); 
      }

      return numberList.toString();
    }
  }
}
</script>
