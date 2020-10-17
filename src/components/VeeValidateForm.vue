<template>
  <div>
    <h2>VeeValidate Form</h2>
    <ValidationObserver v-slot="{ handleSubmit }">
        <form @submit.prevent="handleSubmit(onSubmit)">
            <ValidationProvider name="Name" rules="required|alpha" v-slot="{ errors }">
                <div class="form-group">
                    <label>Name</label>
                    <input type="text" class="form-control" v-model="formData.name">
                    <span>{{ errors[0] }}</span>
                </div>
            </ValidationProvider>

            <ValidationProvider name="E-Mail" rules="required|email" v-slot="{ errors }">
                <div class="form-group">
                    <label>Email</label>
                    <input type="email" class="form-control" v-model="formData.email">
                    <span>{{ errors[0] }}</span>
                </div>
            </ValidationProvider>

            <ValidationProvider name="Password" rules="required|max:12|min:6" v-slot="{ errors }">
                <div class="form-group">
                    <label>Password</label>
                    <input type="password" class="form-control" v-model="formData.password">
                    <span>{{ errors[0] }}</span>
                </div>
            </ValidationProvider>
            
             <ValidationProvider name="Gender" rules="required" v-slot="{ errors }">
                <div class="form-group">
                    <label>Gender</label>
                    <select class="form-control" v-model="formData.gender">
                        <option value="male">Male</option>
                        <option value="female">Female</option>
                        <option value="other">other</option>
                    </select>
                    <span>{{ errors[0] }}</span>
                </div>
            </ValidationProvider>

            <ValidationProvider name="Accept Terms" rules="required" v-slot="{ errors }">
                <div class="form-check">
                    <input type="checkbox" class="form-check-input" v-model="formData.acceptTerms">
                    <label class="form-check-label">Accept Terms</label>
                </div>
                <span>{{ errors[0] }}</span><br>
            </ValidationProvider>
            <input type="submit" class="btn btn-primary mt-3" tect="Submit">
        </form>
    </ValidationObserver>
  </div>
</template>

<script>
export default {
  data: () => ({
    formData: {
      name: "",
      email: "",
      password: "",
      gender: "",
      acceptTerms: null
    }
  }),
  methods: {
      onSubmit() {
          console.log(this.formData);
      }
  }
};
</script>