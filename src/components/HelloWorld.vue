<template>
  <div class="hello">
    <div id="builder"></div>
    <button  @click="test">Test</button>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { Formio, FormioForm } from "formiojs";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      testdata: {"components":[{"label":"Select Boxes","labelPosition":"left-right","optionsLabelPosition":"right","tableView":false,"defaultValue":{"":false,"adád":false,"hieu":false,"en":false},"values":[{"label":"hieu","value":"hieu","shortcut":"N"},{"label":"en","value":"en","shortcut":"E"}],"key":"selectBoxes","properties":{"selectBoxkey2":"Hieu"},"type":"selectboxes","input":true,"inputType":"checkbox"},{"label":"Text Area","autoExpand":false,"tableView":true,"key":"textArea","conditional":{"show":true,"when":"selectBoxes","eq":"en"},"type":"textarea","input":true},{"label":"Submit","action":"url","showValidations":false,"size":"sm","block":true,"shortcut":"B","disableOnInvalid":true,"tableView":false,"key":"submit","properties":{"submitkey1":"valuekey1"},"type":"button","url":"http://hieuctfe.github.io/test","input":true,"headers":[{"header":"","value":""}]}]}
    }
  },
  mounted() {
    // this.builder = Formio.builder(document.getElementById("builder"), this.testdata, {});
    Formio.createForm(document.getElementById('builder'), this.testdata, {});
    
  },
  methods: {
    test() {
      this.builder.then(data => {
        console.log(JSON.stringify(data.schema))
      })
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#builder {
  /* width: 50%; */
  /* float: left; */
}
</style>