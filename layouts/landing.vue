<template>
  <v-app light>
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row no-gutters>
          <v-col cols="12" sm="12" md="12">
            <nuxt />
          </v-col>
        </v-row>
      </v-container>
    </v-content>

    <v-footer padless color="#ffffff" fixed>
      <v-col class="text-center" cols="12">
        <v-spacer /> <v-spacer />
        <small>
          <strong>
            &copy;
            {{ new Date().getFullYear() }} FETCH Project</strong
          ></small
        >
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
export default {}
</script>