<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      <v-card>
        <v-card-title class="headline">
          Vue.js App for Fetch Rewards
        </v-card-title>
        <v-card-text>
          <p>This application will demo the submission of form, I have made use of Vuetify library for styling and axios library to make the API calls </p>
        
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="#4a7515"
            nuxt
            to="/first"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  
  name: 'IndexPage',


  mounted() {
    // this.nav()
    },

      methods: {
      nav() {
        this.$router.push({ path: '/first' })

      },
      loginauth() {

      }
    }
}
</script>
