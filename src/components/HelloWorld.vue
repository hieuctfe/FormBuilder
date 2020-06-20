<template>
  <div class="hello">
    <div id="builder"></div>
  </div>
</template>

<script>
import { Formio } from "formiojs";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  mounted() {
    Formio.builder(document.getElementById("builder"), {}, {});
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#builder {
  width: 50%;
  float: left;
}
</style>
