<template>
  <div class="box">
    <grid-layout :layout.sync="layout" :verticalCompact="false" :col-num="5" :row-height="150" :is-draggable="true" :is-resizable="true" :is-mirrored="false" :vertical-compact="true" :margin="[10, 10]" :use-css-transforms="true">
      <!-- 确保在其他 item 下面，放在第一个的会在最下面 -->
      <grid-item v-for="item in backLayout" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :i="item.i" :key="item.i" :is-draggable="false" :is-resizable="false" class="backGridItem"> </grid-item>

      <!-- 真正的layout数据 -->
      <grid-item v-for="item in layout" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :i="item.i" :key="item.i" class="gridItem"> </grid-item>
    </grid-layout>
  </div>
</template>

<script>
import VueGridLayout from "vue-grid-layout";
export default {
  components: {
    gridLayout: VueGridLayout.GridLayout,
    gridItem: VueGridLayout.GridItem,
  },

  data() {
    return {
      layout: [
        { x: 0, y: 0, w: 1, h: 1, i: "0" },
        { x: 1, y: 0, w: 1, h: 1, i: "1" },
      ],
      backLayout: [
        { x: 0, y: 0, w: 1, h: 1, i: "0" },
        { x: 1, y: 0, w: 1, h: 1, i: "1" },
        { x: 2, y: 0, w: 1, h: 1, i: "2" },
        { x: 3, y: 0, w: 1, h: 1, i: "3" },
        { x: 4, y: 0, w: 1, h: 1, i: "4" },

        { x: 0, y: 1, w: 1, h: 1, i: "10" },
        { x: 1, y: 1, w: 1, h: 1, i: "11" },
        { x: 2, y: 1, w: 1, h: 1, i: "12" },
        { x: 3, y: 1, w: 1, h: 1, i: "13" },
        { x: 4, y: 1, w: 1, h: 1, i: "14" },

        { x: 0, y: 2, w: 1, h: 1, i: "20" },
        { x: 1, y: 2, w: 1, h: 1, i: "21" },
        { x: 2, y: 2, w: 1, h: 1, i: "22" },
        { x: 3, y: 2, w: 1, h: 1, i: "23" },
        { x: 4, y: 2, w: 1, h: 1, i: "24" },

        { x: 0, y: 3, w: 1, h: 1, i: "30" },
        { x: 1, y: 3, w: 1, h: 1, i: "31" },
        { x: 2, y: 3, w: 1, h: 1, i: "32" },
        { x: 3, y: 3, w: 1, h: 1, i: "33" },
        { x: 4, y: 3, w: 1, h: 1, i: "34" },
      ],
    };
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}
</style>

<style scoped>
.box {
  background-color: #031e2c;
  height: 100vh;
}
.backGridItem {
  color: #fff;
  border: dashed #ccc 1px;
}
.gridItem {
  background-color: green;
}
</style>
