<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import * as yup from 'yup';
import _ from 'lodash';
import { useField, useForm } from 'vee-validate';

const validationSchema = yup.object({
  name: yup.string().max(5),
});
const { handleSubmit, errors } = useForm({ validationSchema });
const name = useField('name', undefined, { syncVModel: false });
const { value: nameValue, errorMessage: nameError } = name;
const onSubmit = handleSubmit(values => console.log(values));
const errorsWrapper = ref<{ name?: string }>({});

watchEffect(() => {
  if (!_.isEqual(errors.value, errorsWrapper.value)) {
    errorsWrapper.value = errors.value;
  }
});
</script>

<template>
  <v-form @submit="onSubmit">
    <v-text-field
      type="text"
      label="Removes a space"
      v-model.trim="nameValue"
      :error-messages="nameError"
    /> 
  </v-form>

  <hr><br>

  <v-form @submit="onSubmit">
    <v-text-field
      type="text"
      label="No error output"
      v-model.trim="nameValue"
    />
  </v-form>

  <hr><br>

  <v-form @submit="onSubmit">
    <v-text-field
      type="text"
      label="Uses an errors wrapper"
      v-model.trim="nameValue"
      :error-messages="errorsWrapper.name"
    />
  </v-form>
</template>
