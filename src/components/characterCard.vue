<template>
  <div class="q-pa-md row items-start q-gutter-md">

    <router-link :to="{  name: 'character', params: { id: characterData.id } }">
      <q-card class="my-card">
        <img :src="characterData.image">

        <q-card-section>
          <div class="text-h6">{{ characterData.name }}</div>
          <div class="text-subtitle2"><span class="text-weight-bolder">Estado:</span> {{ characterData.status }}</div>
          <div class="text-subtitle2"><span class="text-weight-bolder">Origen:</span> {{ characterData.origin.name }}</div>
        </q-card-section>
      </q-card>
    </router-link>

  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'characterCard',

  props: {
    characterData: null
  }
})
</script>
