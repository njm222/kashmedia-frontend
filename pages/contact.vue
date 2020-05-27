<template>
  <v-layout>
    <v-flex class="text-center">
      <v-toolbar prominent>
        <v-container class="toolbar-container">
          <v-layout
            justify-center
            align-center
          >
            <v-toolbar-title>{{ contactTitle }}</v-toolbar-title>
            <v-spacer />
            <v-toolbar-items class="align-center">
              <div>
                <span>
                  <a>
                    <v-icon x-large class="mx-4">mdi-youtube</v-icon>
                  </a>
                  <a>
                    <v-icon x-large class="mx-4">mdi-instagram</v-icon>
                  </a>
                </span>
              </div>
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
              {{ contactSubtitle }}
            </div>
          </v-layout>
          <v-divider />
          <v-card-title
            class="contact justify-center"
          >
            {{ contactFormTitle }}
          </v-card-title>
          <v-card class="contact-container" outlined raised>
            <v-form
              v-model="valid"
            >
              <v-container>
                <v-spacer />
                <div>
                  <v-col>
                    <v-text-field
                      v-model="firstname"
                      :rules="nameRules"
                      :counter="20"
                      label="First name"
                      required
                    />
                  </v-col>
                  <v-col>
                    <v-text-field
                      v-model="lastname"
                      :rules="nameRules"
                      :counter="20"
                      label="Last name"
                      required
                    />
                  </v-col>
                </div>
                <v-spacer />
                <div>
                  <v-col>
                    <v-text-field
                      v-model="email"
                      :rules="emailRules"
                      label="E-mail"
                      required
                    />
                  </v-col>
                </div>
                <v-spacer />
                <div>
                  <v-col>
                    <v-text-field
                      v-model="subject"
                      :rules="subjectRules"
                      :counter="30"
                      label="Subject"
                      required
                    />
                  </v-col>
                </div>
                <v-spacer />
                <div>
                  <v-col>
                    <v-textarea
                      v-model="message"
                      :rules="messageRules"
                      :counter="750"
                      label="Message"
                      required
                      auto-grow
                    />
                  </v-col>
                </div>
                <v-spacer />
                <div>
                  <v-col>
                    <v-btn :disabled="!valid" outlined v-bind="size" @click="submit">
                      send
                    </v-btn>
                  </v-col>
                </div>
                <v-spacer />
              </v-container>
            </v-form>
          </v-card>
        </v-container>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import ContactQuery from '~/apollo/queries/contact/contactText'

export default {
  data () {
    return {
      contact: [],
      valid: true,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 20 || 'Name must be less than 20 characters'
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ],
      subject: '',
      subjectRules: [
        v => !!v || 'Subject is required',
        v => v.length <= 30 || 'Subject must be less than 30 characters'
      ],
      message: '',
      messageRules: [
        v => !!v || 'Message is required',
        v => v.length <= 750 || 'Message must be less than 750 characters'
      ]
    }
  },
  apollo: {
    contact: {
      prefetch: true,
      query: ContactQuery
    }
  },
  computed: {
    size () {
      const size = { sm: 'small', lg: 'large', xl: 'x-large' }[this.$vuetify.breakpoint.name]
      return size ? { [size]: true } : {}
    },
    contactTitle () {
      return this.contact.title
    },
    contactSubtitle () {
      return this.contact.subtitle
    },
    contactFormTitle () {
      return this.contact.formTitle
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
  .contact.v-card__title {
    margin: 2rem 2em;
    padding: 0;
  }
  .contact-container {
    margin: 0 5%;
  }
  .contact-container form {
    height: 100%;
  }
  .contact-container form .container {
    height: inherit;
    width: 90%;
    margin: 0 5%;
    display: flex;
    flex-direction: column;
  }
</style>
