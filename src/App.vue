<template>
  <div id="app" class="container mt-5">
    <!-- <vee-validate-form /> -->
    <vuelidate-form />
  </div>
</template>

<script>
// import VeeValidateForm from "./components/VeeValidateForm";
import VuelidateForm from "./components/VuelidateForm";

export default {
  name: "App",
  components: {
    // VeeValidateForm,
    VuelidateForm
  }
};
</script>

<style>
@import url("https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css");
</style>
