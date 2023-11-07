<template>
  <div class="form-wrapper">
    <form-field @field-added="addField" />
    <div class="form-display-wrapper">
      <form-display
        v-for="(field, index) in fields"
        :key="index"
        :fieldType="field.fieldType"
        :label="field.label"
        :fieldName="field.fieldName"
        :options="field.options"
        :userInput.sync="field.userInput"
      />
    </div>
    <!--    <button @click="submitFields" class="custom-button">Submit All</button>
    <button @click="clearFields" class="custom-button">Clear All</button> -->
    <div>
      <button @click="submitAllFields" class="custom-button">Submit All</button>
      <button @click="clearFields" class="custom-button">Clear All</button>
    </div>
    <div v-if="isclicked">{{ formData }}</div>
  </div>
</template>

<script>
import FormField from "@/components/FormField.vue";
import FormDisplay from "@/components/FormDisplay.vue";

export default {
  components: {
    FormField,
    FormDisplay,
  },
  data() {
    return {
      fields: JSON.parse(localStorage.getItem("formFields")) || [],
      isclicked: false,
      formData: {},
      userInput: "",
    };
  },
  methods: {
    addField(field) {
      this.fields.push(field);
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem("formFields", JSON.stringify(this.fields));
    },
    clearFields() {
      this.fields = [];
      this.formData = null;
      this.saveToLocalStorage();
    },
    submitAllFields() {
      this.isclicked = true;
      let formData = {};

      for (const field of this.fields) {
        console.log("aqui", field);
        if (Array.isArray(field.options)) {
          formData[field.fieldName] = field.options.join(",");
        } else {
          formData[field.fieldName] = this.userInput;
        }
      }
      this.formData = formData;
      console.log(this.formData);
    },
  },

  beforeDestroy() {
    this.saveToLocalStorage();
  },
};
</script>
<style>
.form-wrapper {
  display: flex;
  flex-direction: row;
}
.form-display-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.custom-button {
  font-size: 14px;
  padding: 10px 20px;
}
</style>
