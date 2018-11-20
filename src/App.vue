<template>
  <v-app>
    <NotificationDialog></NotificationDialog>
    <div class="main-container">
      <router-view></router-view>
    </div>
  </v-app>
</template>

<script>
  import WebFontLoader from 'webfontloader'
  import NotificationDialog from './components/common/notificationDialog'

  export default {
    name: 'App',
    components: {
      NotificationDialog,
    },
    mounted () {
      WebFontLoader.load({
        google: {
          families: ['Roboto:100,300,400,500,700,900']
        },
        active: this.setFontLoaded
      })
    },
    methods: {
      setFontLoaded () {
        this.$emit('font-loaded')
      }
    }
  }
</script>

<style>
</style>
