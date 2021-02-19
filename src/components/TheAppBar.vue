<template>
  <v-app-bar app color="#FAFAFA" :elevation="0">
    <div class="d-flex align-center">
      <v-img :src="require('../assets/logo.png')" width="50"></v-img>
      <v-row class="text-h5 pl-4">太空编程</v-row>
    </div>

    <v-spacer></v-spacer>
    <v-btn icon to="/">
      <v-icon>mdi-home</v-icon>
    </v-btn>
    <v-btn icon to="/about">
      <v-icon>mdi-help</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";
@Component
export default class TheAppBar extends Vue {}
</script>
