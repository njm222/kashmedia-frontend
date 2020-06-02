<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="clipped"
      fixed
      mini-variant
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
          :ripple="false"
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      :collapse-on-scroll="true"
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer />
      <a href="/" class="banner-title">
        <v-toolbar-title>
          <span v-for="item in titleComputed">
            {{ item }}
          </span>
        </v-toolbar-title>
      </a>
      <v-spacer />
    </v-app-bar>
    <v-content>
      <nuxt />
    </v-content>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: true,
      drawer: false,
      items: [
        {
          icon: 'mdi-home',
          title: 'Home',
          to: '/'
        },
        {
          icon: 'mdi-video',
          title: 'Portfolio',
          to: '/portfolio'
        },
        {
          icon: 'mdi-frequently-asked-questions',
          title: 'Bio',
          to: '/bio'
        },
        {
          icon: 'mdi-message',
          title: 'Contact',
          to: '/contact'
        }
      ],
      miniVariant: false,
      right: true,
      title: 'KASHMEDIA'
    }
  },
  computed: {
    titleComputed () {
      const chars = this.title.split('')
      return chars
    }
  }
}
</script>

<style lang="sass">
  @import '~vuetify/src/styles/styles.sass'
</style>
