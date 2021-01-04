<template>
  <v-card class="mx-auto" max-width="300" :elevation="0">
    <v-list>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title>绘制图表</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item-group v-model="model">
        <v-list-item v-for="(item, i) in items" :key="i">
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title v-text="item.text"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
    <v-card :elevation="0" class="pa-2">
      <v-btn depressed @click="$emit('export')">
        导出图片
      </v-btn>
    </v-card>
  </v-card>
</template>

<script lang="ts">
import { Vue, Component, Ref } from "vue-property-decorator";

@Component({})
export default class LeftNavBar extends Vue {
  items = [
    {
      icon: "mdi-inbox",
      text: "菜单1"
    },
    {
      icon: "mdi-star",
      text: "菜单2"
    },
    {
      icon: "mdi-send",
      text: "菜单3"
    },
    {
      icon: "mdi-email-open",
      text: "菜单4"
    }
  ];
  model = 1;
}
</script>
