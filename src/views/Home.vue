<template>
  <v-card class="content-wrapper" :elevation="0">
    <v-row class="fill-height flex">
      <v-col cols="2" class="pl-0"><LeftNavBar @export="onExport"/></v-col>
      <v-col cols="10" class="pl-0">
        <Canvas ref="canvas" />
      </v-col>
    </v-row>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue, Ref } from "vue-property-decorator";
import Canvas from "@/components/Canvas.vue";
import LeftNavBar from "@/components/LeftNavBar.vue";
@Component({
  components: {
    Canvas,
    LeftNavBar
  }
})
export default class Home extends Vue {
  @Ref() readonly canvas!: Vue;

  onExport() {
    console.log("export");
    (this.canvas as Canvas).exportPhoto();
  }
}
</script>
<style lang="scss" scoped>
.content-wrapper {
  height: 100%;
  padding: 0;
  margin: 0;
  display: flex;
  box-sizing: border-box;
  justify-content: center;
  align-items: center;
  vertical-align: bottom;
}
</style>
