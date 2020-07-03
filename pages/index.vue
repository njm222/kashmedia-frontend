<template>
  <v-layout
    class="landing-content-container"
  >
    <youtube
      v-show="!loading"
      class="background-video"
      player-width="100%"
      player-height="100%"
      :video-id="videoId"
      :player-vars="{ autoplay: 1, controls: 0, loop: 1, modestbranding: 1, rel: 0, playlist: videoId }"
      @ready="ready"
    />
    <div v-show="loading">
      <v-layout
        class="loading-container"
        justify-center
        align-center
      >
        <v-progress-circular
          indeterminate
          color="primary"
        />
      </v-layout>
    </div>
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
      landing: [],
      loading: true
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
    },
    videoId () {
      return this.landing.videoID
    }
  },
  methods: {
    ready () {
      this.loading = false
    }
  }
}
</script>

<style>
  .background-video {
  }
  .loading-container,
  .background-video iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
  }
  .landing-content-container {
    height: 100%;
    padding: 0 5% 1%;
  }
  .landing-content-container .layout {
    z-index: 1;
  }
  .landing-title {
    font-size: 2.5em;
    line-height: 1em;
    font-family: 'Poiret One', cursive;
    font-weight: 400;
  }
  .landing-subtitle {
    font-size: 1.5em;
    letter-spacing: 0.2em;
    line-height: 1em;
    margin-top: 0.3rem;
    font-family: 'Poiret One', cursive;
    font-weight: 400;
    margin-left: 2em;
  }
  @media only screen and (max-width: 425px) {
    .landing-title {
      font-size: 1.3em;
    }
    .landing-subtitle {
      font-size: 0.75em;
    }
  }
</style>
