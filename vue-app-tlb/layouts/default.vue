<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app right/>
    <v-toolbar app class="teal lighten-3">
      <v-toolbar-title>ยินดีต้อนรับ</v-toolbar-title>
      <v-spacer/>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"/>
    </v-toolbar>
    <v-content>
      <nuxt/>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
         { title: 'Home', icon: 'home', url: '/' },
         { title: 'Room', icon: 'update', url: '/table1' },
         { title: 'Booking', icon: 'assignment_turned_in', url: '/booking' },
         { title: 'Chat', icon: 'group', url: '/chat' },
         { title: 'key', icon: 'security', url: '/keyroom' },
         { title: 'Logout', icon: 'lock', url: '/Logout' },
       ],
     }
  },
  computed: {
    online: {
      get() {
        return this.$store.state.online
      },
      set(value) {
        this.$store.commit('setOnline', value)
      },
    },
    drawer: {
      get() {
        return this.$store.state.drawer
      },
      set(value) {
        this.$store.commit('setDrawer', value)
      },
    },
  },

  mounted() {
    this.$store.commit('setOnline', window.navigator.onLine)
    window.addEventListener('offline', this.toggleNetworkStatus)
    window.addEventListener('online', this.toggleNetworkStatus)
  },

  beforeDestroyed() {
    window.removeEventListener('offline', this.toggleNetworkStatus)
    window.removeEventListener('online', this.toggleNetworkStatus)
  },

  methods: {
    toggleNetworkStatus({ type }) {
      this.online = type === 'online'
    },
  },
}
</script>
