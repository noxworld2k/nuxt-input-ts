<template>
  <div class="container">
    <form @submit.prevent="submitForm" class="form-box">
      <TextInput
        type="text"
        label="Car Name*"
        placeholder="Enter car name"
        @update:valid="setIsNameValid"
        @update:value="setCarName"
        :disabled="false"
        :icon="'icon__left'"
      />

      <SelectInput
        label="Car Brand*"
        :options="options"
        @update:valid="setCarBrandSelected"
        @update:value="setSelectedOption"
      />

      <SubmitButton :isDisabled="isDisabled">Submit</SubmitButton>
      <div class="success" v-if="succesMessage">
        <p>
          {{ succesMessage }}
        </p>
      </div>
      * Required fields
    </form>
  </div>
</template>

<script setup lang="ts">
import { options } from "@/data/CarBrands.json";
import { reactive, ref, watch, watchEffect } from "vue";

const isNameValid = ref(false);
const isCarBrandSelected = ref(false);
const isDisabled = ref(true);
const formData = reactive({
  name: "",
  brand: "",
});
const succesMessage = ref("");

const setIsNameValid = (value: boolean) => {
  isNameValid.value = value;
};
const setCarBrandSelected = (value: boolean) => {
  isCarBrandSelected.value = value;
};
const checkInputs = () => {
  isDisabled.value = !(isNameValid.value && isCarBrandSelected.value);
};
const setCarName = (value: string) => {
  formData.name = value;
};
const setSelectedOption = (value: string) => {
  formData.brand = value;
};
const submitForm = () => {
  succesMessage.value = `Your car ${formData.name} from ${formData.brand} has been submitted`;
};

watch([isNameValid, isCarBrandSelected], checkInputs);
watchEffect(() =>
  console.log(
    "isNameValid",
    isNameValid.value,
    "isCarBrandSelected",
    isCarBrandSelected.value,
    "isDisabled",
    isDisabled.value,
    "formData",
    formData.brand,
    formData.name
  )
);
</script>

<style>
.input {
  display: flex;
  flex-direction: column;
  margin: 1rem 0;
}
.form-box {
  width: 300px;
}
.success {
  margin-top: 1rem;
  color: green;
}
</style>
