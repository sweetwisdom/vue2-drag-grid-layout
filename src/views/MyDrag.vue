<template>
  <div>
    <div class="box">
      <grid-layout :layout.sync="store.layout" :col-num="layoutConfig.colNum" :row-height="150" :is-draggable="true" :is-resizable="true" :is-mirrored="false" :vertical-compact="false" :margin="[10, 10]" :use-css-transforms="true">
        <!-- 确保在其他 item 下面，放在第一个的会在最下面 -->
        <grid-item v-for="item in store.backLayout" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :i="item.i" :key="item.i" :is-draggable="false" :is-resizable="false" class="backGridItem"> </grid-item>

        <!-- 真正的layout数据 -->
        <grid-item v-for="item in store.layout" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :i="item.i" :key="item.i + 'a'" class="gridItem">
          <span class="text">{{ item.i }}</span>
          <span class="remove" @click="remove(item.i)">x</span>
        </grid-item>
      </grid-layout>
      <!--  -->
    </div>
    <div class="tool">
      <button @click="add">add</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { GridLayout, GridItem } from "vue-grid-layout";
import { reactive, toRefs, ref, onMounted } from "vue";
const store = ref({
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
});
let mouseXY = { x: null, y: null };
let DragPos = { x: null, y: null, w: 1, h: 1, i: null };
const layoutConfig = ref({
  draggable: true,
  resizable: true,
  colNum: 5,
});
function add() {
  const layout = store.value.layout;
  const layoutconfig = layoutConfig.value;
  const tem = {
    x: 2,
    y: 0,
    w: 1,
    h: 1,
    i: layout.length + 1 + "",
  };
  console.log(tem);

  store.value.layout.push(tem);
}

function remove(val) {
  const layout = store.value.layout;
  const index = layout.findIndex((item) => item.i === val);
  layout.splice(index, 1);
}
onMounted(() => {
  document.addEventListener(
    "dragover",
    function (e) {
      mouseXY.x = e.clientX;
      mouseXY.y = e.clientY;
    },
    false
  );
});
</script>

<style scoped>
body {
  background-color: #031e2c;
}
.box {
  background-color: #031e2c;
  height: 90vh;
}
.backGridItem {
  color: #fff;
  border: dashed #ccc 1px;
}
.gridItem {
  background-color: green;
}
.tool {
  background-color: #031e2c;
  height: 10vh;
}
.droppable-element {
  width: 150px;
  text-align: center;
  background: #fdd;
  border: 1px solid black;
  margin: 10px 0;
  padding: 10px;
}
.remove {
  position: absolute;
  right: 2px;
  top: 0;
  cursor: pointer;
}
</style>
