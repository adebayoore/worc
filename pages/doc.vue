<template>
  <v-card class="mb-12" height="500px">
    <v-form>
      <v-container>
        <v-row>
          <v-col cols="12" md="6">
            <v-file-input
              show-size
              counter
              label="Resume Upload"
              filled
              prepend-icon="mdi-newspaper-variant-outline"
            ></v-file-input> </v-col
          ><v-col cols="12" md="6">
            <v-file-input
              show-size
              counter
              label="Driver's License Upload"
              filled
              prepend-icon="mdi-card-account-details-outline"
            ></v-file-input>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="6">
            <v-file-input
              show-size
              counter
              label="Birth Certificate Upload"
              filled
              prepend-icon="mdi-certificate"
            ></v-file-input> </v-col
          ><v-col cols="12" md="6">
            <v-file-input
              show-size
              counter
              label="Proof of Address"
              filled
              prepend-icon="mdi-home"
            ></v-file-input>
          </v-col>
        </v-row>
      </v-container> </v-form
  ></v-card>
</template>

<script>
export default {
  layout: "emp"
};
</script>

