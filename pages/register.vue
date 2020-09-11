<template>
  <v-col class="text-center">
    <span class="bg"></span>
    <v-snackbar class="text-center"
      v-model="snackbar"
      outlined
    >{{ error }}</v-snackbar>
    <v-snackbar class="text-center"
      v-model="snackbar2"
      outlined
    >Account Created!</v-snackbar>


    <v-card width="400" class="mx-auto mt-5">
      <v-col class="text-center">
        <v-card-title class="pb-0" center>
          <p class="text-right">Sign-Up</p>
        </v-card-title>
      </v-col>
      <v-progress-linear
        :active="loading"
        :indeterminate="loading"
        absolute
        bottom
        color="deep-purple accent-4"
      ></v-progress-linear>
      <v-card-text>
        <v-form
          v-if="step === steps.register"
          @submit.prevent="register"
          ref="form"
        >
          <v-text-field
            v-model="registerForm.email"
            type="email"
            placeholder="Email"
            class="form-control"
            prepend-icon="mdi-email"
          />
          <v-text-field
            :rules="rules"
            v-model="registerForm.password"
            :type="showPassword ? 'text' : 'password'"
            label="Password"
            prepend-icon="mdi-lock"
            class="form-control"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
          />
          <v-text-field
            v-model="match"
            :type="showPassword ? 'text' : 'password'"
            label="Confirm Password"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
          />
          <v-divider></v-divider>
            <v-card-action>
            <v-btn type="submit" text color="success">
              Sign Up
            </v-btn>
            <nuxt-link to="/login">Have an account? Login</nuxt-link>
          </v-card-action>
        </v-form>

       
        <!-- Confirm Registration -->
        <form v-else @submit.prevent="confirm">
          <v-text-field v-model="confirmForm.email" type="email" placeholder="Email" class="form-control" />
          <v-text-field v-model="confirmForm.code" placeholder="Code" class="form-control" />
          <v-btn type="submit" text>Confirm</v-btn>
          <v-spacer></v-spacer>
          <span>Please check your email for the confirmation code</span>  
        </form>

      </v-card-text>
    </v-card>
      
    <v-overlay :value="overlay">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </v-col>

</template>
<script>
const steps = {
  register: 'REGISTER',
  confirm: 'CONFIRM'
}
export default {
  data: () => ({
    showPassword: false,
    snackbar: false,
    snackbar2: false,
    overlay: false,

    steps: { ...steps },
    step: steps.register,
    match: '',

    registerForm: {
      email: '',
      password: ''
    },
    confirmForm: {
      email: '',
      code: ''
    }
  }),
  computed: {
    rules() {
      const rules = []

      if (this.match) {
        const rule = v =>
          (!!v && v) === this.match || 'The passwords do not match'

        rules.push(rule)
      }

      return rules
    }
  },

  watch: {
    match: 'validateField',
    max: 'validateField',
    model: 'validateField',

    overlay (val) {
      val && setTimeout(() => {
        this.overlay = false
      }, 3000)
    },
  },

  methods: {
    validateField() {
      this.$refs.form.validate()
    },

    async register() {
      try {
        await this.$store.dispatch('auth/register', this.registerForm)
        this.confirmForm.email = this.registerForm.email
        this.step = this.steps.confirm
        this.loading= true;
      } catch (error) {
        console.log({ error })
        this.snackbar= true;
        this.error= error.message;

      }
    },

    async confirm() {
      try {
        await this.$store.dispatch('auth/confirmRegistration', this.confirmForm)
        await this.$store.dispatch('auth/login', this.registerForm)
        this.$router.push('/')
        this.snackbar2= true;

      } catch (error) {
        this.snackbar= true;
        console.log({ error })
      }
    }
  }
}
</script>

<style scoped>
.bg {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background: url('https://images.unsplash.com/photo-1527401850656-0f34108fdb30?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60')
    no-repeat center center;
  background-size: cover;
  /* background-color: red; */
  transform: scale(1.1);
}
</style>
