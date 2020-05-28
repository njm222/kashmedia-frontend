<template>
  <v-layout
    class="landing-content-container"
  >
    <v-layout
      column
      justify-end
      align-start
    >
      <h1 class="landing-title font-weight-bold">
        {{ landingTitle }}
      </h1>
      <h2 class="landing-subtitle font-weight-thin">
        {{ landingSubtitle }}
      </h2>
    </v-layout>
    <v-layout
      justify-center
      align-end
    >
      <v-btn
        to="/portfolio"
        outlined
        v-bind="size"
      >
        Portfolio
      </v-btn>
    </v-layout>
  </v-layout>
</template>

<script>
import LandingQuery from '~/apollo/queries/landing/landingText'

export default {
  data () {
    return {
      landing: []
    }
  },
  apollo: {
    landing: {
      prefetch: true,
      query: LandingQuery
    }
  },
  computed: {
    size () {
      const size = { sm: 'small', lg: 'large', xl: 'x-large' }[this.$vuetify.breakpoint.name]
      return size ? { [size]: true } : {}
    },
    landingTitle () {
      return this.landing.title
    },
    landingSubtitle () {
      return this.landing.subtitle
    }
  }
}
</script>

<style>
  .landing-content-container {
    height: 100%;
    padding: 0 5% 2%;
  }
  .landing-title {
    font-size: 6vw;
    line-height: 1em;
  }
  .landing-subtitle {
    font-size: 4vw;
    line-height: 1em;
    margin-top: .5em;
  }
</style>
