<template>
  <v-layout v-if="Object.keys(bio).length > 1">
    <v-flex class="text-center">
      <v-toolbar prominent>
        <v-container class="toolbar-container">
          <v-layout
            justify-center
            align-center
          >
            <v-toolbar-title>
              {{ bioTitle }}
            </v-toolbar-title>
            <v-spacer />
            <v-toolbar-items>
              sample bio item
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
              {{ bioSubtitle }}
            </div>
          </v-layout>
          <v-divider />
          <v-layout v-if="Object.keys(bio).length > 4" class="bio-container text-left" align-center>
            <v-card-text>
              <p style="white-space: pre-line;">
                {{ bioContent }}
              </p>
            </v-card-text>
            <v-card-text>
              <v-img
                :src="bioImage.url"
                :lazy-src="bioImage.url"
                aspect-ratio="1"
                max-width="400"
              >
                <template v-slot:placeholder>
                  <v-row
                    class="fill-height ma-0"
                    align="center"
                    justify="center"
                  >
                    <v-progress-circular indeterminate color="primary" />
                  </v-row>
                </template>
              </v-img>
            </v-card-text>
          </v-layout>
        </v-container>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import BioQuery from '~/apollo/queries/bio/bioText'

export default {
  data () {
    return {
      bio: {}
    }
  },
  apollo: {
    bio: {
      prefetch: true,
      query: BioQuery
    }
  },
  computed: {
    size () {
      const size = { sm: 'small', lg: 'large', xl: 'x-large' }[this.$vuetify.breakpoint.name]
      return size ? { [size]: true } : {}
    },
    bioTitle () {
      return this.bio.title
    },
    bioSubtitle () {
      return this.bio.subtitle
    },
    bioContent () {
      return this.bio.bioContent
    },
    bioImage () {
      console.log(this.bio)
      console.log(this.bio.bioImage)
      return this.bio.bioImage
    }
  }
}
</script>

<style>
  .bio-container .v-card__text {
    padding: 5vw;
  }
  @media only screen and (max-width: 768px) {
    .bio-container {
      flex-direction: column;
    }
  }
</style>
