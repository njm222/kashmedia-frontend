<template>
  <v-layout>
    <v-flex class="text-center">
      <v-toolbar prominent>
        <v-container class="toolbar-container">
          <v-layout
            justify-center
            align-center
          >
            <v-toolbar-title>Contact</v-toolbar-title>
            <v-spacer/>
            <v-toolbar-items class="align-center">
              <v-row>
                <span>
                  <a>
                    <v-icon x-large class="mx-4">mdi-youtube</v-icon>
                  </a>
                  <a>
                    <v-icon x-large class="mx-4">mdi-instagram</v-icon>
                  </a>
                </span>
              </v-row>
            </v-toolbar-items>
          </v-layout>
        </v-container>
      </v-toolbar>
      <div>
        <v-container>
          <v-layout
            justify-center
            align-center
          >
            <div class="pre-quote">
              Here's a showcase of my work filler text and some more text for two lines of my work filler text.
            </div>
          </v-layout>
          <v-divider/>
          <v-card class="contact-container">
            <v-card-title
              class="justify-center"
            >
              Drop me a message
            </v-card-title>
            <v-form
              v-model="valid"
            >
              <v-container>
                <v-row>
                  <v-col>
                    <v-text-field
                      v-model="firstname"
                      :rules="nameRules"
                      :counter="10"
                      label="First name"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col>
                    <v-text-field
                      v-model="lastname"
                      :rules="nameRules"
                      :counter="10"
                      label="Last name"
                      required
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col>
                    <v-text-field
                      v-model="email"
                      :rules="emailRules"
                      label="E-mail"
                      required
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col>
                    <v-text-field
                      v-model="subject"
                      :rules="subjectRules"
                      :counter="30"
                      label="Subject"
                      required
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col>
                    <v-text-area
                      v-model="message"
                      :rules="messageRules"
                      :counter="500"
                      label="Message"
                      required
                    ></v-text-area>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col>
                    <v-btn :disabled="!valid" class="mr-4" @click="submit">submit</v-btn>
                  </v-col>
                  <v-col>
                    <v-btn @click="clear">clear</v-btn>
                  </v-col>
                </v-row>
              </v-container>
            </v-form>
          </v-card>
        </v-container>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>

export default {
  data() {
    return {
      valid: true,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      subject: '',
      subjectRules: [
        v => !!v || 'Subject is required',
        v => v.length <= 30 || 'Subject must be less than 30 characters',
      ],
      message: '',
      messageRules: [
        v => !!v || 'Message is required',
        v => v.length <= 500 || 'Message must be less than 500 characters',
      ]
    }
  },
  methods: {
    submit () {
      console.log(this.firstname)
      console.log(this.lastname)
      console.log(this.email)
      console.log(this.subject)
      console.log(this.message)
    },
    clear () {
      this.firstname = ''
      this.lastname = ''
      this.email = ''
      this.subject = ''
      this.message = ''
      this.valid = true
    }
  }
}
</script>

<style>
  .contact-container {
    margin: 3rem 0;
  }
</style>
