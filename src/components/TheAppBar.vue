<template>
  <v-app-bar app color="#FAFAFA" :elevation="0">
    <div class="d-flex align-center">
      太空编程
    </div>

    <v-spacer></v-spacer>

    <v-btn icon to="/about">
      <v-icon>mdi-help</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";
@Component({})
export default class TheFooter extends Vue {}
</script>
