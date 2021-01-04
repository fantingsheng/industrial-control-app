<template>
  <v-footer class="px-1" app padless>
    <v-col cols="5" class="py-2 status">{{ status }}</v-col>
    <v-col cols="2" class="py-2" align="center">
      <span v-if="timeVisible">{{ timeText }}</span>
    </v-col>
    <v-col
      cols="5"
      class="py-2 text-right text-overline font-weight-regular"
      align="end"
      >@{{ new Date().getFullYear() }} 太空编程</v-col
    >
  </v-footer>
</template>

<script lang="ts">
import { Vue, Component, Prop, Watch } from "vue-property-decorator";

import moment from "moment";

@Component
export default class TheFooter extends Vue {
  @Prop({ type: String, default: "" }) readonly status!: string;
  @Prop({ type: Boolean, default: true }) readonly time!: boolean;

  timeText = "";
  timeVisible = this.time;

  updateInterval_: NodeJS.Timeout | null = null;

  update(): void {
    this.timeText = moment().format("ddd HH:mm A");
    if (this.timeVisible) {
      if (this.updateInterval_ === null) {
        this.updateInterval_ = setInterval(this.update, 1000);
      }
    } else {
      this.clearUpdateInterval();
    }
  }

  mounted(): void {
    this.update();
  }

  beforeDestroy(): void {
    this.clearUpdateInterval();
  }

  @Watch("time")
  onTimeChanged(val: boolean): void {
    this.timeVisible = val;
    this.update();
  }

  clearUpdateInterval(): void {
    if (this.updateInterval_ !== null) {
      clearInterval(this.updateInterval_);
      this.updateInterval_ = null;
    }
  }
}
</script>
