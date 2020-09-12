<template>
  <v-container fill-height fluid grid-list-xl>
    <v-layout justify-center wrap>
      <v-flex xs12 md8>
        <v-form ref="form" v-model="valid" lazy- readonly>
          <v-container py-0>
            <v-layout wrap>
              <v-flex xs12 md4>
                <v-text-field
                  label="First Name"
                  v-model="firstname"
                  :rules="nameRules"
                />
              </v-flex>
              <v-flex xs12 md4>
                <v-text-field
                  class="purple-input"
                  label="Last Name"
                  :rules="nameRules"
                  v-model="lastname"
                />
              </v-flex>
              <v-flex xs12 md4>
                <v-text-field v-model="email" disabled class="purple-input">
                </v-text-field>
              </v-flex>
              <v-flex xs12 md6>
                <v-select
                  v-model="education"
                  :items="schoollevel"
                  :rules="nameRules"
                  label="Current Level of Education"
                  required
                ></v-select>
              </v-flex>
              <v-flex xs12 md6>
                <v-select
                  v-model="foi"
                  :items="field"
                  :rules="nameRules"
                  label="Field of Interest"
                  required
                ></v-select>
              </v-flex>
              <v-flex xs12 md12>
                <v-text-field
                  v-model="school"
                  label="Name of School"
                  class="purple-input"
                />
              </v-flex>

              <v-flex xs12 md6>
                <v-select
                  v-model="town"
                  :items="districts"
                  :rules="nameRules"
                  label="Where are you?"
                  required
                ></v-select>
              </v-flex>

              <v-flex xs12 md6>
                <v-menu
                  v-model="menu2"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  transition="scale-transition"
                  offset-y
                  min-width="290px"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="date"
                      label="Select An Available Start Date For Work"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="date"
                    @input="menu2 = false"
                  ></v-date-picker>

                  
                </v-menu>
              </v-flex>
              <v-flex xs12>
                <v-textarea
                  v-model="bio"
                  :rules="[v => !!v || 'Required']"
                  class="purple-input"
                  label="About Me"
                  placeholder="Tell us about yourself"
                />
              </v-flex>
              <v-file-input
                label="Upload A PDF Of Your Most Recent Resume"
                show-size
                filled
                prepend-icon="mdi-paperclip"
              ></v-file-input>

              <v-flex xs12 text-xs-right>
                <v-btn
                  v-on:click="createProfile"
                  text
                  class="mx-0 font-weight-light"
                  color="success"
                  outlined
                >
                  Update Profile
                </v-btn>
                <v-btn
                  text
                  class="mx-0 font-weight-light"
                  color="info"
                  outlined
                >
                  View
                </v-btn>
              </v-flex>
            </v-layout>
          </v-container>
        </v-form>
      </v-flex>
      <v-flex xs12 md4>
        <material-card class="v-card-profile">
          <div class="text-center">
            <v-avatar color="red" size="62">
              <span class="white--text headline">AO</span>
            </v-avatar>
          </div>
          <v-card-text class="text-xs-center">
            <h5 class="category text-gray font-weight-thin mb-3">
              {{ education }} {{ foi }} - {{ town }}
            </h5>

            <h3 class="card-title font-weight-light">
              {{ firstname }} {{ lastname }}
            </h3>
            <v-spacer></v-spacer>
            <p class="card-description font-weight-light">
              {{ bio }}
            </p>
          </v-card-text>
        </material-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
// import { API } from 'aws-amplify'
// import { createProfile } from '../src/graphql/mutations'
export default {
  layout: 'emp',
  data() {
    return {
      firstname: 'Adebayo',
      lastname: 'Oremule',
      bio: '',
      school: 'John Gray High School',
      foi: 'Accounting',
      education: 'High School',
      date: '',
      date2: '',
      town: 'Cayman Brac',
      nameRules: [v => !!v || 'Required'],
      bioRules: [
        v => !!v || 'Required',
        v => (v && v.length > 10) || 'Bio must be more than 10 characters'
      ],
      dates: ['2019-09-10', '2019-09-20'],
      menu2: false,
      menu3: false,
      modal: false,
     

      schoollevel: [
        'High School',
        '6th Form',
        'Undergraduate',
        'Post Graduate'
      ],
      districts: [
        'Grand Cayman',
        'Cayman Brac',
        'Little Cayman',
        'United Kingdom',
        'United States',
        'Canada'
      ],
      field: [
        'Accounting',
        'Business',
        'Marketing',
        'Technology',
        'Law',
        'Construction',
        'Human Resources',
        'Project Management'
      ]
    }
  },
  methods: {
    async createProfile() {
      const {
        firstname,
        lastname,
        school,
        bio,
        foi,
        education,
        date,
        town
      } = this
      if (
        !firstname ||
        !lastname ||
        !school ||
        !bio ||
        !foi ||
        !education ||
        !date ||
        !town
      )
        return
      const profile = {
        firstname,
        lastname,
        school,
        bio,
        foi,
        education,
        date,
        town
      }
      await API.graphql({
        query: createProfile,
        variables: { input: profile }
      })
      this.firstname = ''
      this.lastname = ''
      this.school = ''
      this.bio = ''
      this.foi = ''
      this.education = ''
      this.date = ''
      this.town = ''
    }
  }
}
</script>
