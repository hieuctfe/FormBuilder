<template>
  <div class="hello">
    <button @click="formBuilder">Form builder (create JSON)</button>
    <button @click="jsonToForm">JSON to form</button>
    <div style="margin-top: 50px" v-show="tab == 'builder'">
      <div id="builder"></div>
      <textarea
        style="display: block; width: 100%"
        rows="6"
        v-model="jsonDataModel"
      />
    </div>
    <div style="margin-top: 50px" v-show="tab == 'form'">
      <div id="form"></div>
      <textarea
        style="display: block; width: 100%"
        rows="6"
        v-model="jsonDataModel"
      />
    </div>
    <!-- <button @click="test">Test</button> -->
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
      dataModel: {
        components: [
          {
            label: "Select Boxes",
            labelPosition: "left-right",
            optionsLabelPosition: "right",
            tableView: false,
            defaultValue: { "": false, adád: false, hieu: false, en: false },
            values: [
              { label: "hieu", value: "hieu", shortcut: "N" },
              { label: "en", value: "en", shortcut: "E" },
            ],
            key: "selectBoxes",
            properties: { selectBoxkey2: "Hieu" },
            type: "selectboxes",
            input: true,
            inputType: "checkbox",
          },
          {
            label: "Text Area",
            autoExpand: false,
            tableView: true,
            key: "textArea",
            conditional: { show: true, when: "selectBoxes", eq: "en" },
            type: "textarea",
            input: true,
          },
          {
            label: "Submit",
            action: "url",
            showValidations: false,
            size: "sm",
            block: true,
            shortcut: "B",
            disableOnInvalid: true,
            tableView: false,
            key: "submit",
            properties: { submitkey1: "valuekey1" },
            type: "button",
            url: "http://hieuctfe.github.io/test",
            input: true,
            headers: [{ header: "", value: "" }],
          },
        ],
      },
      tab: "builder",
    };
  },
  computed: {
    jsonDataModel: {
      get: function() {
        return JSON.stringify(this.dataModel) || "";
      },
      // setter
      set: function(newValue) {
        this.dataModel = JSON.parse(newValue);
      },
    },
  },
  mounted() {
    this.formBuilder();
  },
  methods: {
    test() {},
    jsonToForm() {
      this.tab = "form";
      this.$nextTick(() => {
        this.form = Formio.createForm(
          document.getElementById("form"),
          this.dataModel,
          {}
        );
      });
    },
    formBuilder() {
      this.tab = "builder";
      this.builder = Formio.builder(
        document.getElementById("builder"),
        this.dataModel,
        {}
      );
    },
    generateJson() {
      this.builder.then((data) => {
        console.log(JSON.stringify(data.schema));
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#builder {
  /* width: 50%; */
  /* float: left; */
}
</style>
