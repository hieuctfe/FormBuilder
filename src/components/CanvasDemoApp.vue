<template>
  <div class="demo-container">
    <div class="canvas-container">
      <CanvasFrame :list-shape="listShape" />
      <MovePoint
        v-for="(position, key) in listShape.path"
        :key="key"
        :position="position"
        @change="(position) => updateData(position, key)"
      />
    </div>
  </div>
</template>

<script>
import CanvasFrame from "./canvas";
import MovePoint from "./move";
export default {
  name: "CanvasDemoApp",
  props: {
    msg: String,
  },
  components: { CanvasFrame, MovePoint },
  data() {
    return {
      listShape: {
        path: [
          {
            left: 100,
            top: 0,
          },
          {
            left: 60,
            top: 90,
          },
          {
            left: 90,
            top: 150,
          },
          {
            left: 300,
            top: 200,
          },
        ],
      },
    };
  },
  mounted() {},
  methods: {
    updateData({ left, top }, index) {
      this.listShape.path[index].left = left;
      this.listShape.path[index].top = top;
    },
  },
};
</script>

<style scoped>
.canvas-container {
  width: fit-content;
  height: fit-content;
  position: relative;
  margin: auto;
}
.demo-container {
  text-align: center;
}
</style>
