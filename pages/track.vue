<template>
  <div class="container mt-5">
      <v-dialog v-model="dialog" max-width="600px">
        <v-card>
          <v-container style="max-width: 500px;">
            <v-container style="max-width: 700px;">
              <v-flex xs12 offset-xs10>
                <v-card width="max" class="mx-auto" />
              </v-flex>
            </v-container>
          </v-container>
        </v-card>
      </v-dialog>
    <div class="row">
      <div class="col form-inline"></div>
    </div>
    <div class="row mt-5">
      <div class="col-3">
        <div class="p-2 alert alert-secondary">
          <h3>Personal Details</h3>
          <draggable
            class="list-group kanban-column"
            :list="profiles"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="item in profiles"
              :key="item.id"
            >
              <v-container grid-list-md>
                <v-card class="mx-auto" max-width="344" outlined>
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="overline mb-4">
                        {{ item.firstname }} {{ item.lastname }}
                      </div>
                      <v-list-item-title class="headline mb-1">{{
                        item.foi
                      }}</v-list-item-title>
                      <v-list-item-subtitle>{{
                        item.education
                      }}</v-list-item-subtitle>
                    </v-list-item-content>

                    <v-btn icon>
                      <v-icon>
                        mdi-account-details-outline
                      </v-icon>
                    </v-btn>
                  </v-list-item>

                  <v-card-actions> </v-card-actions>
                </v-card>
              </v-container>
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 alert alert-primary">
          <h3>Document Uploads</h3>
          <!-- In Progress draggable component. Pass arrInProgress to list prop -->
          <draggable
            class="list-group kanban-column"
            :list="arrInProgress"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="item in arrInProgress"
              :key="item.id"
              justify-space-between
            >
              <div>
                <v-container grid-list-md>
                  <v-card
                    class="pa mx-auto"
                    max-width="344"
                    outlined
                    color="error"
                  >
                    <v-list-item three-line>
                      <v-list-item-content>
                        <div class="overline mb-4">
                          {{ item.firstname }} {{ item.lastname }}
                        </div>
                        <v-list-item-title class="headline mb-1">{{
                          item.foi
                        }}</v-list-item-title>
                        <v-list-item-subtitle>{{
                          item.education
                        }}</v-list-item-subtitle>
                      </v-list-item-content>
                      <v-btn icon v-on="on" @click="dialog = true">
                        <v-icon>
                          mdi-account-details-outline
                        </v-icon>
                      </v-btn>

                      <!-- <v-list-item-avatar
                    tile
                    size="80"
                    color="grey"
                  ></v-list-item-avatar> -->
                    </v-list-item>

                    <v-card-actions> </v-card-actions>
                  </v-card>
                </v-container>
              </div>
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 alert alert-warning">
          <h3>Verification</h3>
          <!-- TestingOn-Boar draggable component. Pass arrTested to list prop -->
          <draggable
            class="list-group kanban-column"
            :list="arrTested"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="item in arrTested"
              :key="item.id"
            >
              <v-container grid-list-md>
                <v-card
                  class="mx-auto"
                  max-width="344"
                  outlined
                  color="warning"
                >
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="overline mb-4">
                        {{ item.firstname }} {{ item.lastname }}
                      </div>
                      <v-list-item-title class="headline mb-1">{{
                        item.foi
                      }}</v-list-item-title>
                      <v-list-item-subtitle>{{
                        item.education
                      }}</v-list-item-subtitle>
                    </v-list-item-content>
                    <v-btn icon>
                      <v-icon>
                        mdi-account-details-outline
                      </v-icon>
                    </v-btn>
                  </v-list-item>

                  <v-card-actions> </v-card-actions>
                </v-card>
              </v-container>
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 alert alert-success">
          <h3>Done</h3>
          <!-- Done draggable component. Pass arrDone to list prop -->
          <draggable
            class="list-group kanban-column"
            :list="arrDone"
            group="tasks"
          >
            <div class="list-group-item" v-for="item in arrDone" :key="item.id">
              <v-container grid-list-md>
                <v-card
                  class="mx-auto"
                  max-width="344"
                  outlined
                  color="success"
                >
                  <v-list-item three-line>
                    <v-list-item-content>
                      <div class="overline mb-4">
                        {{ item.firstname }} {{ item.lastname }}
                      </div>
                      <v-list-item-title class="headline mb-1">{{
                        item.foi
                      }}</v-list-item-title>
                      <v-list-item-subtitle>{{
                        item.education
                      }}</v-list-item-subtitle>
                    </v-list-item-content>
                    <v-btn icon @click.stop="dialog = true">
                      <v-icon>
                        mdi-account-details-outline
                      </v-icon>
                    </v-btn>
                  </v-list-item>
                  <v-card-actions> </v-card-actions>
                </v-card>
              </v-container>
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import { API } from 'aws-amplify'
import draggable from 'vuedraggable'
// import { getProfile } from '../src/graphql/queries'
// import { listProfiles } from '../src/graphql/queries'
// import { onCreateProfile } from '../src/graphql/subscriptions'

export default {
  layout: 'emp',
  name: 'kanban-board',
//   async created() {
//     this.getProfiles()
//     this.subscribe()
//   },
  components: {
    //import draggable as a component
    draggable
  },
  data: () => ({
    return: {
      dialog: 'false',
      dialog2: 'false'
    },

    firstname: '',
    lastname: '',
    bio: '',
    school: '',
    foi: '',
    education: '',
    date: '',
    town: '',
    profiles: [],
    // for new tasks
    newTask: '',
    // 4 arrays to keep track of our 4 statuses
    arrBackLog: [
      

    ],
    arrInProgress: [{firstname: 'Patrick',lastname: 'Richards' ,foi:'Accounting', education:'Post Graduate'}],
    arrTested: [{firstname: 'Sandra',lastname: 'Seymour' ,foi:'App Developer', education:'High School'}],
    arrDone: []
  }),

  methods: {
    async getProfiles() {
      const profiles = await API.graphql({
        query: listProfiles
      })
      this.profiles = profiles.data.listProfiles.items
    },

    subscribe() {
      API.graphql({ query: onCreateProfile }).subscribe({
        next: eventData => {
          let profile = eventData.value.data.onCreateProfile
          if (this.profiles.some(item => item.name === profile.name)) return // remove duplications
          this.profiles = [...this.profiles, profile]
        }
      })
    }
  }
}
</script>

<style>
/* light stylings for the kanban columns */
.kanban-column {
  min-height: 300px;
}
</style>
