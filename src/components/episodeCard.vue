<template>
  <q-card class="my-card">
    <q-card-section>
      <div class="text-subtitle2"><span class="text-weight-bolder">{{ nameEpisode }}</span></div>
      <div class="text-subtitle2">{{ dateEpisode }}</div>
    </q-card-section>
  </q-card>
</template>

<script>
import { defineComponent } from 'vue';
import { api } from 'boot/axios';

export default defineComponent({
  name: 'episodeCard',

  props: {
    urlEpisode: null
  },

  data() {
    return {
      nameEpisode: null,
      dateEpisode: null
    }
  },

  mounted() {
    this.loadData(this.urlEpisode);
  },

  methods: {
    loadData(url) {
      api.get(url)
        .then(response => {
          this.nameEpisode = response.data.name;
          this.dateEpisode = response.data.air_date;
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
});
</script>
