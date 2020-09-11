<template>
  <div id="app">
    <v-app id="inspire">
      <div>
        <v-card class="mb-4">
          <v-card-text>
            <v-select
              v-model="steps"
              :items="[1, 2, 3, 4]"
              label="Number of steps to complete application process?"
            ></v-select>
          </v-card-text>
        </v-card>
        <v-card width="mx-auto">
          <v-stepper v-model="e1" vertical>
            <template v-for="n in steps">
              <v-stepper-step
                :key="`${n}-step`"
                :step="n"
                :complete="e1 > n"
                editable
              >
                Step {{ n }}
              </v-stepper-step>
              <v-stepper-content :step="n" :key="`${n}-content`">
                <v-card class="mb-5" height="450">
                  <p>
                    + to add fields for data entry
                  </p>

                  <v-from>
                    <div
                      v-for="(textField, i) in textFields"
                      :key="i"
                      class="text-fields-row"
                    >
                      <v-text-field
                        :label="textField.label1"
                        v-model="textField.value1"
                        :append-icon="mdi-close"
                        @click:append="remove(i)"
                      ></v-text-field>
                      
                    </div>
                    <v-btn @click="add" outlined icon
                      ><v-icon>mdi-plus</v-icon></v-btn
                    >
                  </v-from>
                </v-card>

                <v-btn color="primary" @click="nextStep(n)">Save</v-btn>
                <v-btn flat @click="dialog = true">Done</v-btn>
              </v-stepper-content>
            </template>
          </v-stepper>
        </v-card>
      </div>

      <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-card-title class="headline grey lighten-2" primary-title>
          Attention <v-spacer></v-spacer> <v-icon>mdi-alert</v-icon>
        </v-card-title>

        <v-card-text> By clicking I Agree, you hearby agree and consent to the terms and conditions of using the Scholarship portal.</v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn color="primary" text @click="dialog2 = true">
            Read Terms
          </v-btn>
          <v-spacer></v-spacer>

          <v-btn color="success" text to="/home">
            I Agree & Next
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
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
          
        </v-toolbar>
        <v-list three-line subheader>
          <v-subheader>Terms and Conditions</v-subheader>
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
    </v-app>
  </div>
</template>
<script>
export default {
  layout: 'emp',
  data() {
    return {
      dialog: false,
      dialog2: false,
      textFields: [],
      e1: 1,
      steps: 1
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
    add() {
      this.textFields.push({
        label1: 'Label',
        value1: 'Text'
      })
    },
    remove(index) {
      this.textFields.splice(index, 1)
    },

    onInput(val) {
      this.steps = parseInt(val)
    },
    nextStep(n) {
      if (n === this.steps) {
        this.e1 = 1
      } else {
        this.e1 = n + 1
      }
    }
  }
}
</script>
