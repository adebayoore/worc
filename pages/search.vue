<template>
  <v-card>
    <v-col v-for="(item, i) in items" :key="i" cols="12">
      <v-card :color="item.color" dark>
        <div class="d-flex flex-no-wrap justify-space-between">
          <div>
            <v-card-title class="headline" v-text="item.title"></v-card-title>

            <v-card-subtitle v-text="item.artist"></v-card-subtitle>
            <v-btn text color='success'>APPLY</v-btn>
          </div>

          <v-avatar class="ma-3" size="125" tile>
            <v-img :src="item.src"></v-img>
          </v-avatar>
        </div>
      </v-card>
    </v-col>
  </v-card>
</template>

<script>
export default {
    layout: 'emp',
    data: () => ({
      items: [
        {
          src: 'https://cdn.vuetifyjs.com/images/cards/mountain.jpg',
          title: 'CUC',
          artist: 'HR Manager',
        },
        {
          src: 'https://cdn.vuetifyjs.com/images/cards/mountain.jpg',
          title: 'Water Authority',
          artist: 'Plant Worker',
        },
      ],
    }),
  }
</script>

<style></style>
