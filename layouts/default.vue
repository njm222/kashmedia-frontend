<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      :collapse-on-scroll=true
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-content>
      <nuxt />
    </v-content>
    <v-footer>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
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
          icon: 'mdi-apps',
          title: 'Sample',
          to: '/home'
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
          icon: 'mdi-frequently-asked-questions',
          title: 'Contact',
          to: '/contact'
        }
      ],
      miniVariant: false,
      right: true,
      title: 'KASHMEDIA'
    }
  }
}
</script>
