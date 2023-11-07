<template>
  <div class="form-display">
    <div v-if="fieldType === 'text'">
      <label>{{ fieldName }}</label>
      <input :type="fieldType" :name="fieldName" v-model="userInput" />
    </div>
    <div v-else-if="fieldType === 'number'">
      <label>{{ fieldName }}</label>
      <input :type="fieldType" :name="fieldName" v-model="userInput" />
    </div>
    <div v-else-if="fieldType === 'select'">
      <label>{{ fieldName }}</label>
      <select :name="fieldName" v-model="userInput">
        <option v-for="(opt, index) in options" :key="index">{{ opt }}</option>
      </select>
    </div>

    <div class="buttons-wrapper">
      <button class="m-l-20 m-r-20" @click="clearFields">Clear</button>
      <button @click="submitFields">Submit</button>
    </div>
    <div v-if="isclicked">{{ formData }}</div>
  </div>
</template>

<script>
export default {
  props: {
    fieldType: String,
    label: String,
    fieldName: String,
    options: Array,
  },
  data() {
    return {
      userInput: "",
      isclicked: false,
      formData: {},
    };
  },
  methods: {
    clearFields() {
      this.userInput = "";
      this.formData = null;
    },
    submitFields() {
      this.isclicked = true;
      this.formData = {
        [this.fieldName]: this.userInput,
      };
      console.log(this.formData);
      return this.formData;
    },
  },
};
</script>

<style>
.form-display {
  width: 50%;
}
.buttons-wrapper {
  display: flex;
}
.m-l-20 {
  margin-left: 20px;
}

.m-r-20 {
  margin-right: 20px;
}
</style>
