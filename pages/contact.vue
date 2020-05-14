<template>
  <v-layout>
    <v-flex class="text-center">
      <v-toolbar>
        <v-toolbar-title>Drop me a message</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
          <v-layout justify-center align-center>
            contact info section
          </v-layout>
        </v-toolbar-items>
      </v-toolbar>
      <v-container>
        <v-layout>
          contact info section
        </v-layout>
      </v-container>
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
              <v-text-field
                v-model="message"
                :rules="messageRules"
                :counter="500"
                label="Message"
                required
              ></v-text-field>
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
