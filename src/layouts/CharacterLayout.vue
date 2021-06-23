<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          aria-label="Menu"
        />

        <q-toolbar-title>
            <router-link to="/">
                Rick and Morty
            </router-link>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <!-- <router-view /> -->
      <character />
    </q-page-container>
  </q-layout>
</template>

<script>

import { defineComponent } from 'vue'

import Character from '../pages/Character.vue';

export default defineComponent({
  name: 'CharacterLayout',

  components: {
    Character
  },

})
</script>