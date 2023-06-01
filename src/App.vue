<script setup lang="ts">
import { useField, useForm } from 'vee-validate';

const { handleSubmit } = useForm();
const name = useField('name', undefined, { syncVModel: false });
const { value: nameValue, errorMessage: nameError } = name;
const onSubmit = handleSubmit(values => console.log(values));

</script>

<template>
  <v-form @submit="onSubmit">
    <v-text-field type="text" v-model.trim="nameValue" :error-messages="nameError" /> 
  </v-form>

  <hr><br>

  <v-form @submit="onSubmit">
    <v-text-field type="text" v-model.trim="nameValue" />
  </v-form>
</template>
