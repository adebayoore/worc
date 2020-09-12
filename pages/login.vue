<template>
  <v-col class="text-center">
    <span class="bg"></span>
    <v-card width="400" class="mx-auto mt-5">
      <v-col>
        <v-card-title class="pb-0" center>
          <p class="text-right">Sign-in</p>
        </v-card-title>
      </v-col>
      <v-overlay :value="overlay">
        <v-progress-circular indeterminate size="64"></v-progress-circular>
      </v-overlay>
      <v-card-text>
        <v-form @submit.prevent="login" ref="form">
          <v-text-field
            v-model="form.email"
            type="email"
            label="Email"
            prepend-icon="mdi-email"
            class="form-control"
          />

          <v-text-field
            v-model="form.password"
            :type="showPassword ? 'text' : 'password'"
            label="Password"
            prepend-icon="mdi-lock"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
            class="form-control"
          />

          <v-divider></v-divider>

          <v-card-action>
            <v-btn text color="error" to="/">
              Back
            </v-btn>
            <v-btn type="submit" text color="info">Login</v-btn>
            <v-btn text color="info" to="home">skip</v-btn>
          </v-card-action>
        </v-form>
      </v-card-text>
      <div v-if="snackbar">
        <spacer></spacer>
        <v-card>
          <nuxt-link to="/register">
            Not Registered? Click here
          </nuxt-link>
        </v-card>
      </div>
    </v-card>
    <v-snackbar v-model="snackbar" outlined>
      The details you've provided don't match any of our records. Try again
    </v-snackbar>

    <div></div>
  </v-col>
</template>

<script>


export default {
  data: () => ({
    
    showPassword: false,
    snackbar: false,
    overlay: false,
    form: {
      email: '',
      password: ''
    }
  }),

  // watch: {
  //   overlay(val) {
  //     val &&
  //       setTimeout(() => {
  //         this.overlay = false
  //       }, 2500)
  //   }
  // },

  methods: {
    async login() {
      try {
        await this.$store.dispatch('auth/login', this.form)
        this.$router.push('/bulletin')
        this.overlay = true
      } catch (error) {
        console.log({ error })
        console.log('Wrong')
        this.snackbar = true
        this.error = error.message
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
