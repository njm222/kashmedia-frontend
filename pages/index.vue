<template>
  <v-layout
  fill-height>
    <v-layout
      column
      justify-end
      align-start
      class="mb-5 ml-5"
    >
      <h1 class="display-4 font-weight-bold">{{landingTitle}}</h1>
      <h2 class="display-1 font-weight-thin">{{landingSubtitle}}</h2>
    </v-layout>
    <v-layout
    justify-center
    align-end
    class="mb-5"
    >
      <v-btn
        to="/portfolio"
        outlined>
        Portfolio
      </v-btn>
    </v-layout>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'
import LandingQuery from '~/apollo/queries/landing/landingText'

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  data() {
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
    landingTitle: function () {
      return this.landing.title

    },
    landingSubtitle: function () {
      return this.landing.subtitle
    }
  }
}
</script>
