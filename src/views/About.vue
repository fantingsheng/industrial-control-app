<template>
  <v-container class="ma-0 pa-0" fill-height fluid>
    <v-card
      class="about ma-auto"
      min-width="400"
      min-height="250"
      flat
      outlined
    >
      <v-card-title>关于</v-card-title>
      <div class="d-flex flex-no-wrap justify-space-between">
        <v-avatar class="ma-3" size="60" tile>
          <v-img :src="require('../assets/logo.png')"></v-img>
        </v-avatar>
        <v-card-text>
          <div no-gutters v-for="(v, k) in versions" :key="k">
            <span>{{ k }}</span
            >: {{ v }}
          </div>
        </v-card-text>
      </div>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import Vuetify from "vuetify";

@Component
export default class About extends Vue {
  get versions() {
    return {
      app: "1.0.0",
      vue: Vue.version,
      vuetify: Vuetify.version
    };
  }
}
</script>

<style lang="scss" scoped>

.v-card__text {
  padding-top: 0;
  padding-bottom: 0;

  div span {
    text-transform: capitalize;
  }

  div:last-child {
    margin-top: 4px;
  }
}
</style>
