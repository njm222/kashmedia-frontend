<template>
  <v-layout>
    <v-flex class="text-center">
      <v-toolbar prominent>
        <v-container class="toolbar-container">
          <v-layout
            justify-center
            align-center
          >
            <v-toolbar-title>
              Portfolio
            </v-toolbar-title>
            <v-spacer />
            <v-toolbar-items>
              <v-select
                v-model="defaultCategory"
                item-text="name"
                :label="defaultCategory.name"
                :items="videoCategories"
                class="d-flex align-center"
                outlined
                color="primary"
                transition="scroll-y-transition"
              />
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
          <v-divider />
          <div ref="portfolioContainer">
            <div v-for="(video, index) in videosByCategory" :key="video.link">
              <div class="my-8">
                <div ref="portfolioItems" class="item-container">
                  <v-layout
                    v-if="loading[index] === true"
                    justify-center
                    align-center
                  >
                    <v-progress-circular
                      indeterminate
                      color="primary"
                    />
                  </v-layout>
                  <youtube
                    :class="{ visible: !loading[index] }"
                    :video-id="video.link"
                    player-width="100%"
                    player-height="100%"
                    class="youtube-container"
                    @ready="ready(index)"
                  />
                  <v-spacer />
                  <v-layout column class="text-left" justify-center>
                    <v-card-title>{{ video.title }}<br>{{ video.subtitle }}</v-card-title>
                    <v-card-text>{{ video.description }}</v-card-text>
                  </v-layout>
                </div>
              </div>
              <div>
                <v-divider />
              </div>
            </div>
          </div>
        </v-container>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import videosQuery from '~/apollo/queries/video/videos'
import videoCategoriesQuery from '~/apollo/queries/video/categories'

export default {
  data () {
    return {
      // Initialize an empty videos variable
      model: 'tab-portfolio-videos',
      videos: [],
      videoCategories: [],
      defaultCategory: 'all',
      loading: []
    }
  },
  computed: {
    videosByCategory () {
      return this.videos.filter((video) => {
        return video.video_categories.some((category) => {
          return category.name === this.defaultCategory
        })
      })
    }
  },
  mounted () {
    this.updatePortfolioItemsCount()
  },
  apollo: {
    videos: {
      prefetch: true,
      query: videosQuery
    },
    videoCategories: {
      prefetch: true,
      query: videoCategoriesQuery
    }
  },
  methods: {
    ready (index) {
      this.$nextTick(this.$set(this.loading, index, false))
    },
    updatePortfolioItemsCount () {
      const numOfVideos = this.videos.length
      for (let i = 0; i < numOfVideos; i++) {
        this.loading[i] = true
      }
    }
  }
}
</script>

<style>
  .item-container {
    width: 100%;
    max-width: 100vw;
    display: flex;
    flex-direction: row;
  }
  .item-container .layout {
    width: 48%;
    margin: 0 1%;
  }
  .youtube-container {
    align-self: center;
    width: 48%;
    margin: 0 1%;
    height: 0;
    z-index: 1;
    position: relative;
    padding-bottom: 27%;
    display: none;
    overflow: hidden;
  }
  .youtube-container.visible {
    display: block;
  }
  .youtube-container iframe {
    display: block;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 5;
    position: absolute;
  }
  .v-select {
    min-width: 20rem;
  }
  .v-select.v-text-field input {
    width: 0;
  }
  @media only screen and (max-width: 768px) {
    .v-select {
      min-width: 16rem;
    }
    .item-container {
      flex-direction: column;
      text-align: center;
    }
    .youtube-container {
      width: 90%;
      margin: 0 5%;
      padding-bottom: 50.625%;
    }
    .item-container .layout {
      width: 90%;
      margin: 0 5%;
    }
  }
</style>
