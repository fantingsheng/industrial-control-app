<template>
  <v-card class="fill-height">
    <Canvas />
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Canvas from "@/components/Canvas.vue"; // @ is an alias to /src

@Component({
  components: {
    Canvas
  }
})
export default class Home extends Vue {}
</script>
