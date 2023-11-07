<template>
  <div class="add-field">
    <div class="add-field-wrapper">
      <label>Select type of field: </label>
      <select v-model="fieldType" class="m-b-20">
        <option value="text">Text</option>
        <option value="number">Number</option>
        <option value="Select">Select</option>
      </select>
      <label>Label: </label>
      <input v-model="label" :placeholder="Label" class="m-b-20" />
      <label>Field Name: </label>
      <input
        v-model="fieldName"
        :placeholder="fieldName"
        label="Field Name"
        class="m-b-20"
      />
      <label>Options: </label>
      <select
        v-model="options"
        placeholder="Options"
        label="Options"
        class="m-b-20"
        :disabled="fieldType != 'Select'"
      >
        <option v-for="(opt, index) in fields" :key="index">{{ opt }}</option>
      </select>
    </div>
    <div class="button-wrapper">
      <button @click="addField">Add Field</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fieldName: "",
      fieldType: "text",
      label: "",
      options: [],
    };
  },
  methods: {
    addField() {
      const field = {
        fieldName: this.fieldName,
        fieldType: this.fieldType,
        label: this.label,
        options: this.options,
      };
      this.$emit("field-added", field);
      this.fieldName = "";
      this.label = "";
      this.options = "";
    },
  },
};
</script>
<style>
.add-field {
  width: 25%;
  padding: 80px 80px 80px 80px;
}

.add-field-wrapper {
  display: flex;
  flex-direction: column;
}
.m-b-20 {
  margin-bottom: 20px;
}

.button-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
