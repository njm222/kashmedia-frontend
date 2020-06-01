<template>
  <v-layout
    class="landing-content-container"
  >
    <v-layout
      column
      justify-end
      align-start
    >
      <h1 class="landing-title">
        {{ landingTitle }}
      </h1>
      <h2 class="landing-subtitle">
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
    font-size: 7.5vw;
    line-height: 1em;
    font-family: 'Poiret One', cursive;
    font-weight: 400;
  }
  .landing-subtitle {
    font-size: 3.5vw;
    letter-spacing: 0.2em;
    line-height: 1em;
    margin-top: .5em;
    font-family: 'Poiret One', cursive;
    font-weight: 400;
  }
</style>
