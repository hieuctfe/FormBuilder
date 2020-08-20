<template>
  <div ref="move-ele" class="move-ele"></div>
</template>

<script>
import Draggabilly from "draggabilly";
export default {
  name: "Canvas",
  props: {
    position: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    style() {
      const { left, top } = this.position;
      return {
        left: `${left - this.pointSize / 2}px`,
        top: `${top - this.pointSize / 2}px`,
        width: `${this.pointSize}`,
        height: `${this.pointSize}`,
      };
    },
  },
  data() {
    return {
      pointSize: 14,
    };
  },
  mounted() {
    let elem = this.$refs["move-ele"];
    this.drag = new Draggabilly(elem, {
      containment: ".canvas-container",
    });
    this.drag.setPosition(
      this.position.left - this.pointSize / 2,
      this.position.top - this.pointSize / 2
    );
    this.drag.on("dragMove", () => {
      const left = this.drag.position.x + this.pointSize / 2;
      const top = this.drag.position.y + this.pointSize / 2;
      this.$emit("change", {
        left: left,
        top: top,
      });
    });
  },
  methods: {},
};
</script>

<style scoped>
.move-ele {
  width: 15px;
  height: 15px;
  background-color: rgba(44, 44, 66, 0.5);
  position: absolute;
  border-radius: 50%;
}
.move-ele:hover {
  cursor: pointer;
}
</style>
