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
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <!--    スナックバー   ー-->
    <!--    <v-snackbar v-model="snackbarVisible" top>-->
    <!--      {{ this.$store.getters['snackbar/message'] }}-->
    <!--    </v-snackbar>-->
    <global-snackbar />
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import GlobalSnackbar from '../components/GlobalSnackbar'

export default {
  components: { 'global-snackbar': GlobalSnackbar },
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'careLog',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Calender',
          to: '/calender/calender',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Note',
          to: '/note/note',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'apolloLocalStateTest',
          to: '/storeTests/apolloLocalStateTest',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'apolloCacheTest',
          to: '/storeTests/apolloCacheTest',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'vuexTest',
          to: '/storeTests/vuexTest',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'vuetifyValidation',
          to: '/validationTest/vuetifyValidation',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'veeValidationTest',
          to: '/validationTest/veeValidationTest',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'mockServerTest',
          to: '/mockServerTest',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'yorisoi-demo',
    }
  },
  computed: {
    // snackbarが自動でfalseに設定するためセッタを用意して、明示的にdispatchからOffするようにする
    snackbarVisible() {
      return this.$store.state.snackbar.isEnable
    },
  },
}
</script>
