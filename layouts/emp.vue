<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
    <span>Employee Side</span>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
      
      <v-divider></v-divider>
        <span></span>
          Client Side
       <v-list>
        <v-list-item
          v-for="(item, i) in item2"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>

    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-toolbar-title v-text="title" />
      
      <v-spacer />
      <v-btn icon to="/">
          <v-icon>
              mdi-home
          </v-icon>
      </v-btn>
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy;Orem</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      items: [
        {
          icon: 'mdi-account',
          title: 'Profile',
          to: '/profile'
        },
        {
          icon: 'mdi-progress-alert',
          title: 'Application Status',
          to: '/status'
        },
        {
          icon: 'mdi-folder',
          title: 'Document Uploads',
          to: '/doc'
        },
        {
          icon: 'mdi-briefcase-search',
          title: 'Job Search',
          to: '/search'
        }
      ],
      item2: [
        {
          icon: 'mdi-playlist-edit',
          title: 'Manage Postings',
        },
        {
          icon: 'mdi-script',
          title: 'Job Post',
          to: '/jobpost'
        },
        {
          icon: 'mdi-progress-clock',
          title: 'Applicant Tracking',
          to: '/track'
        },
      ],
      title: 'Welcome Ade'
    }
  }
}
</script>
