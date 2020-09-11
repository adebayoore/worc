<template>
  <div id="app">
    <form @submit.prevent="handleSubmit">
      <v-card>
        <v-toolbar>
          <v-toolbar-title>Job Post</v-toolbar-title>
          <v-spacer></v-spacer>

          <v-btn text outlined v-on:click="createTodo" @click="dialog = true">
            create
          </v-btn>
          <v-toolbar-items> </v-toolbar-items>
        </v-toolbar>
        <v-list>
          <v-list-item>
            <v-list-item-content>
              <v-text-field
                v-model="name"
                :rules="[v => !!v || 'Required']"
                type="text"
                label="Job Title"
                placeholder="Required"
                outlined
                shaped
              ></v-text-field>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-content>
              <v-textarea
                :rules="[v => !!v || 'Required']"
                label="Description"
                type="text"
                v-model="description"
                outlined
                placeholder="Required"
                shaped
              ></v-textarea>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-content>
              <v-text-field
                label="URL"
                type="text"
                v-model="url"
                outlined
                placeholder="Example: https://www.companyname.com/careers/scholarships/ "
                shaped
              ></v-text-field>
            </v-list-item-content>
          </v-list-item>
        </v-list>
        <v-divider></v-divider>
        <v-list three-line subheader>
          <v-subheader>Targeted Qualifications</v-subheader>
          <v-list-item>
            <v-col class="d-flex" cols="12" sm="6">
              <v-radio-group v-model="column" column>
                <v-radio label="High School" value="Full-Time"></v-radio>
                <v-radio label="Undergraduate" value="Part-Time"></v-radio>
                <v-radio label="Post-Graduate" value="Internship"></v-radio>
              </v-radio-group>
            </v-col>

            <v-col>
              <v-file-input
                label="Logo"
                filled
                prepend-icon="mdi-camera"
              ></v-file-input>

              <v-menu
                ref="menu"
                v-model="menu"
                :close-on-content-click="false"
                :return-value.sync="deadline"
                transition="scale-transition"
                offset-y
                min-width="290px"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="deadline"
                    label="Deadline"
                    prepend-icon="mdi-calendar"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker v-model="deadline" no-title scrollable>
                  <v-spacer></v-spacer>
                  <v-btn text color="primary" @click="menu = false"
                    >Cancel</v-btn
                  >
                  <v-btn text color="primary" @click="$refs.menu.save(deadline)"
                    >Save</v-btn
                  >
                </v-date-picker>
              </v-menu>
            </v-col>
            <spacer></spacer>
          </v-list-item>
        </v-list>        

        <div></div>
        <v-snackbar v-model="snackbar" :timeout="timeout">
          Go to 'Manage Listings' in order to make changes or track analytics
          <v-btn color="blue" text @click="snackbar = false">Close</v-btn>
        </v-snackbar>
      </v-card>
    </form>
    <v-dialog
      v-model="dialog2"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
    >
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="dialog2 = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>Data Privacy</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items>
            <v-btn dark text @click="dialog = false">I Agree</v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-list three-line subheader>
          <v-subheader>Terms and Conditions for WORC</v-subheader>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title>Introduction</v-list-item-title>
              <v-list-item-subtitle> </v-list-item-subtitle>
              These Website Standard Terms and Conditions written on this
              webpage shall manage your use of our website, Webiste Name
              accessible at Website.com. These Terms will be applied fully and
              affect to your use of this Website. By using this Website, you
              agreed to accept all terms and conditions written in here. You
              must not use this Website if you disagree with any of these
              Website Standard Terms and Conditions.
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title>Your Content</v-list-item-title>
              <v-list-item-subtitle> </v-list-item-subtitle> In these Website
              Standard Terms and Conditions, “Your Content” shall mean any
              audio, video text, images or other material you choose to display
              on this Website. By displaying Your Content, you grant Company
              Name a non-exclusive, worldwide irrevocable, sub licensable
              license to use, reproduce, adapt, publish, translate and
              distribute it in any and all media. Your Content must be your own
              and must not be invading any third-party's rights. Company Name
              reserves the right to remove any of Your Content from this Website
              at any time without notice. If any provision of these Terms is
              found to be invalid under any applicable law, such provisions
              shall be deleted without affecting the remaining provisions
              herein. Variation of Terms Company Name is permitted to revise
              these Terms at any time as it sees fit, and by using this Website
              you are expected to review these Terms on a regular basis.
              Assignment The Company Name is allowed to assign, transfer, and
              subcontract its rights and/or obligations under these Terms
              without any notification. However, you are not allowed to assign,
              transfer, or subcontract any of your rights and/or obligations
              under these Terms. Entire Agreement These Terms constitute the
              entire agreement between Company Name and you in relation to your
              use of this Website, and supersede all prior agreements and
              understandings. Governing Law & Jurisdiction These Terms will be
              governed by and interpreted in accordance with the laws of the
              State of Country, and you submit to the non-exclusive jurisdiction
              of the state and federal courts located in Country for the
              resolution of any disputes.
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-card>
    </v-dialog>

    <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-card-title class="headline grey lighten-2" primary-title>
          Attention <v-spacer></v-spacer> <v-icon>mdi-alert</v-icon>
        </v-card-title>

        <v-card-text> By clicking I Agree, you hearby agree and consent to the terms and conditions of using the WORC Job portal.</v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn color="primary" text @click="dialog2 = true">
            Read Terms
          </v-btn>
          <v-spacer></v-spacer>

          <v-btn color="success" text to="sworkflow">
            I Agree & Next
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
// import { API } from 'aws-amplify'
// import { createTodo } from '../src/graphql/mutations'

export default {
  layout: 'emp',
  data() {
    return {
      dialog: false,
      dialog2: false,
      e1: 1,
      steps: 2,
      date: new Date().toISOString().substr(0, 10),
      menu: false,
      name: '',
      description: '',
      url: '',
      deadline: '',
      date: null,
      timeout: 4000,
      menu: false,
      e1: 1,
      steps: 2,
      e7: [],
      keywords: [
        'Finance',
        'Culinary',
        'Service Industry',
        'Technology',
        'Health Care',
        'Business',
        'Law',
        'Accounting'
      ],
      snackbar: false,
      timeout: 2500
    }
  },
  watch: {
    steps(val) {
      if (this.e1 > val) {
        this.e1 = val
      }
    }
  },
  methods: {
    nextStep(n) {
      if (n === this.steps) {
        this.e1 = 1
      } else {
        this.e1 = n + 1
      }
    },

    async createTodo() {
      const { name, description, deadline, url } = this
      if (!name || !description || !deadline || !url) return
      const todo = { name, description, deadline, url }
      await API.graphql({
        query: createTodo,
        variables: { input: todo }
      })
      this.name = ''
      this.description = ''
      this.deadline = ''
      this.url = ''
    }
  }
}
</script>
