<template>
  <v-timeline align-top :dense="$vuetify.breakpoint.smAndDown">
    <v-timeline-item
      v-for="(item, i) in item2"
      :key="i"
      :color="item.color"
      :icon="item.icon"
      fill-dot
    >
      <v-card :color="item.color" dark>
        <v-card-title class="title">{{ item.text }}</v-card-title>
        <v-card-text class="white text--primary">
          <p>
            Lorem ipsum dolor sit amet, no nam oblique veritus. Commune scaevola
            imperdiet nec ut, sed euismod convenire principes at. Est et nobis
            iisque percipit, an vim zril disputando voluptatibus, vix an
            salutandi sententiae.
          </p>
          <v-btn
            icon
            :color="item.color"
            class="mx-0"
            outlined
            @click="dialog = true"
          >
            <v-icon>mdi-check-decagram</v-icon>
          </v-btn>
        </v-card-text>
      </v-card>
    </v-timeline-item>

    <v-timeline-item
      v-for="(item, i) in items"
      :key="i"
      :color="item.color"
      :icon="item.icon"
      fill-dot
    >
      <v-card :color="item.color" dark>
        <v-card-title class="title">{{ item.text }}</v-card-title>
        <v-card-text class="white text--primary">
          <p>
            Lorem ipsum dolor sit amet, no nam oblique veritus. Commune scaevola
            imperdiet nec ut, sed euismod convenire principes at. Est et nobis
            iisque percipit, an vim zril disputando voluptatibus, vix an
            salutandi sententiae.
          </p>
          <v-btn icon :color="item.color" class="mx-0" outlined @click="dialog2 = true">
            <v-icon>mdi-account-clock</v-icon>
          </v-btn>
        </v-card-text>
      </v-card>
    </v-timeline-item>
    <v-snackbar v-model="dialog"><span>Verified by: Delicia Brown</span></v-snackbar>
    <v-snackbar v-model="dialog2"><span>This Step Is Pending Verification</span></v-snackbar>
  </v-timeline>
</template>

<script>
export default {
  layout: "emp",
  data: () => ({
    dialog: false,
    dialog2: false,
    items: [
      {
        text: "Document Verification",
        color: "grey",
        icon: "mdi-star"
      },
      {
        text: "Citizenship",
        color: "grey",
        icon: "mdi-book-variant"
      },
      {
        text: "Place Holder",
        color: "grey",
        icon: "mdi-airballoon"
      },
      {
        text: "Place Holder",
        color: "grey",
        icon: "mdi-buffer"
      }
    ],

    item2: [
      {
        text: "Personal Details",
        color: "indigo",
        icon: "mdi-account"
      }
    ]
  })
};
</script>
