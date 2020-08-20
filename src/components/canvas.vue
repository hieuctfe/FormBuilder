<template>
  <!-- <canvas ref="canvasRef" width="500px" height="500px" class="canvas"></canvas> -->
  <img
    ref="image"
    :src="require('@/assets/E8UV4J4BZ-W011PQ0FCMC-a776a541c918-512.jpeg')"
    crossorigin="anonymous"
    class="image"
  />
</template>

<script>
import Cropper from "cropperjs";
export default {
  name: "Canvas",
  props: {
    listShape: {
      type: Object,
      default: () => {},
    },
    options: {
      aspectRatio: NaN,
      checkCrossOrigin: false,
      zoomOnWheel: false,
      movable: false,
      autoCropArea: 1,
      viewMode: 1,
    },
  },
  data() {
    return {};
  },

  computed: {
    image() {
      return this.$refs.image;
    },
  },
  mounted() {
    // this.drawShape();
    this.cropper = new Cropper(this.image, this.options);
  },
  methods: {
    drawShape() {
      const canvas = this.$refs["canvasRef"];
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, 500, 500);
      const { path } = this.listShape;
      // this.listShape.forEach(({ path }) => {
      if (path && path.length) {
        ctx.beginPath();
        ctx.moveTo(path[0].left, path[0].top);
        path.forEach((point, index) => {
          if (index > 0) {
            ctx.lineTo(point.left, point.top);
          }
        });
        ctx.fill();
      }
    },
  },
  watch: {
    listShape: {
      deep: true,
      handler: function() {
        // this.drawShape();
        const { path } = this.listShape;
        let temp = path.map(point => `${point.left}px ${point.top}px`).join(',');
        this.image.setAttribute('style',`clip-path: polygon(${temp})`);
      },
    },
  },
};
</script>

<style scoped>
.canvas {
  width: 500px;
  height: 500px;
  border: 1px solid #ccc;
}
/* img {
  position: absolute;
  top: 10px;
  left: 10px;
  right: 10px;
  bottom: 10px;
  background-color: #d3d0c9;
  background-image: url(pics/pittsburgh.jpg);
  background-size: cover;
  background-position: center center;
} */
</style>
