<template>
  <q-page class="container-sm">
    <div class="row flex-center">
      <div class="col-8 q-mt-md q-mb-md">
        <q-input outlined v-model="search" @update:model-value="searchEvent()" label="Buscar..." />
      </div>
    </div>
    <div class="row flex-center">
      <div class="col-3">
        Filtrar por:
      </div>
      <div class="col-3">
        <q-select
          outlined
          v-model="statusFilter"
          :options="statusFilterOptions"
          option-label="name"
          map-options
          label="Status"
          @update:model-value="statusFilterEvent()"
        />
      </div>
      <div class="col-3">
        <q-select outlined v-model="originFilter" :options="originFilterOptions" label="Origin" />
      </div>
    </div>
    <div class="row flex-center">
      <character-card 
        v-for="(character, index) in characters" 
        :key="index"
        :characterData="character"
      />
    </div>
    <!-- <div class="row flex-center">
      <q-pagination
        v-model="currentPage"
        :max="5"
        direction-links
      />
    </div> -->
  </q-page>
</template>

<script>
import { api } from 'boot/axios';

import characterCard from '../components/characterCard.vue';

export default {
  name: 'PageIndex',

  components: {
    characterCard,
  },

  data() {
    return {
      characters: [],
      search: null,
      statusFilter: null,
      statusFilterOptions: [
        {
          id: 'alive',
          name: 'alive'
        },
        {
          id: 'dead',
          name: 'dead'
        },
        {
          id: 'unknown',
          name: 'unknown'
        }
      ],
      originFilter: null,
      originFilterOptions: [],
    }
  },
  
  mounted() {
    this.getCharacters();
    this.getLocations();
    console.log('index');
  },

  methods: {
    getCharacters() {
      api.get('/character')
        .then(response => {
          this.characters = response.data.results;
        })
        .catch(err => {
          console.log(err)
        });
    },
    statusFilterEvent() {
      api.get(`/character/?status=${this.statusFilter.name}`)
        .then(response => {
          this.characters = response.data.results;
        })
        .catch(err => {
          console.log(err)
        });
    },
    searchEvent() {
      api.get(`/character/?name=${this.search}`)
        .then(response => {
          this.characters = response.data.results;
        })
        .catch(err => {
          console.log(err)
        });
    },
    getLocations() {
      api.get('/location')
        .then(response => {
          this.originFilterOptions = response.data.results;
        })
        .catch(err => {
          console.log(err)
        });
    }
  },
}
</script>
