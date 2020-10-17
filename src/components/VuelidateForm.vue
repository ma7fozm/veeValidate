<template>
  <div>
    <h2>Vuelidate Form</h2>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label>Name</label>
        <input type="text" v-model="name" class="form-control" />
        <span v-if="!$v.name.required && $v.name.$dirty" class="text-danger">Name is required!</span>
        <span v-if="!$v.name.alpha && $v.name.$dirty" class="text-danger">Name is required!</span>
      </div>

      <div class="form-group">
        <label>Email</label>
        <input type="email" v-model="email" class="form-control" />
        <span
          v-if="(!$v.email.required || !$v.email.email) && $v.email.$dirty"
          class="text-danger"
        >Valid Email is required!</span>
      </div>

      <div class="form-group">
        <label>Password</label>
        <input type="password" v-model="password" class="form-control" />
        <span
          v-if="!$v.password.required && $v.password.$dirty"
          class="text-danger"
        >Password is required!</span>
        <span
          v-if="(!$v.password.minLength || !$v.password.maxLength) && $v.password.$dirty"
          class="text-danger"
        >Password must be between {{ $v.password.$params.minLength.min}} and {{ $v.password.$params.maxLength.max}} characters!</span>
      </div>
      <div class="form-group">
        <label for>Gender</label>
        <select v-model="gender" class="form-control">
          <option value="male">Male</option>
          <option value="female">Female</option>
          <option value="other">Other</option>
        </select>
        <span v-if="!$v.gender.required && $v.gender.$dirty" class="text-danger">Gender is required!</span>
      </div>
      <div class="form-check">
        <input type="checkbox" v-model="acceptTerms" class="form-check-input" />
        <label for="" class="form-check-label">Accept Terms</label>
      </div>
      <span v-if="!$v.acceptTerms.required && $v.acceptTerms.$dirty" class="text-danger">Accept Terms is required!</span>
       <br> <input type="submit" class="btn btn-primary mt-2">
    </form>
  </div>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  alpha,
  email
} from "vuelidate/lib/validators";
export default {
  data: () => ({
    name: "",
    email: "",
    password: "",
    gender: "",
    acceptTerms: ""
  }),
  validations: {
    name: {
      required,
      alpha
    },
    email: {
      required,
      email
    },
    password: {
      required,
      maxLength: maxLength(12),
      minLength: minLength(6)
    },
    gender: {
      required
    },
    acceptTerms: {
      required
    }
  },
  methods: {
    submitForm() {
      this.$v.$touch();

      if (!this.$v.$invalid) {
        console.log(
          `Name: ${this.name}, Email: ${this.email}, Password: ${this.password}, Gender: ${this.gender}, Accept Terms: ${this.acceptTerms}`
        );
      }
    }
  }
};
</script>

<style scoped>
</style>