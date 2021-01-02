<template>
  <v-app>
    <TheAppBar />

    <v-main class="mx-4">
      <router-view v-if="routerVisible"></router-view>
    </v-main>

    <TheFooter />
  </v-app>
</template>

<script lang="ts">
import { Vue, Component, Provide, Ref, Watch } from "vue-property-decorator";
import TheAppBar from "./components/TheAppBar.vue";
import TheFooter from "./components/TheFooter.vue";

@Component({
  components: {
    TheAppBar,
    TheFooter
  }
})
export default class App extends Vue {
  routerVisible = true;
}
</script>
