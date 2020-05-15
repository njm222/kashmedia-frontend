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
            <v-spacer/>
            <v-toolbar-items>
              <v-select
                item-text="name"
                v-model="defaultCategory"
                :label="defaultCategory.name"
                :items="videoCategories"
                class="d-flex align-center"
                outlined
                transition="scroll-y-transition"
              ></v-select>
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
          <div v-for="video in videosByCategory" :key="video.link">
            <v-row class="my-8">
              <v-layout>
                <youtube :video-id="video.link" player-width="100%" player-height="100%" class="youtube-container col-5"></youtube>
                <v-layout column class="col-6 offset-1 text-left" justify-center>
                  <v-card-title>{{video.title}}</v-card-title>
                  <v-card-text>{{video.description}}</v-card-text>
                </v-layout>
              </v-layout>
            </v-row>
            <v-row>
              <v-divider/>
            </v-row>
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
  data() {
    return {
      // Initialize an empty videos variable
      model: 'tab-portfolio-videos',
      videos: [],
      videoCategories: [],
      defaultCategory: 'all'
    }
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
  computed: {
    videosByCategory: function () {
      return this.videos.filter((video) => {
        return video.video_categories.some((category) => {
          return category.name === this.defaultCategory
        })
      })
    }
  },
}
</script>

<style>
  .youtube-container {
    width: 100%;
    height: 0;
    margin: auto;
    z-index: 1;
    position: relative;
    padding-bottom: 23.4375%;
    display: block;
    overflow: hidden;
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
  .v-text-field .v-input__control {
    height: 3.5rem;
  }
  .v-select {
    min-width: 20rem;
  }
  .v-select.v-text-field input {
    width: 0;
  }
</style>
