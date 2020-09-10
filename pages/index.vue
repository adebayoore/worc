<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <div class="text-center">
        <img height="200px" src="@/assets/kygov.jpg"/>
        <div class="text-center">
        <span>Welcome to the Cayman Island's WORC Portal</span>
        </div>
        <!-- <vuetify-logo /> -->
      </div>
      <v-card>
        <!-- <v-card-title class="headline">
          
        </v-card-title> -->
        <v-card-text>
         <img height="200px" src="@/assets/process.png"/>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  }
}
</script>
