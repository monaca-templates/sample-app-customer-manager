<template>
  <v-alert
    transition="slide-y-transition"
    class="notification-dialog"
    v-model="rendered"
    :type="type"
  >
    {{ message }}
  </v-alert>
</template>

<script>
  import { EventBus } from '../../eventBus.js'

  export default {
    name: 'NotificationDialog',
    data: () => {
      return {
        rendered: false,
        message: 'hello',
        type: 'success'
      }
    },
    created () {
      // norify イベントを登録し、発火を検知するとダイアログを表示する
      EventBus.$on('notify', (message, type) => {
        this.message = message
        this.type = type
        this.rendered = true
        setTimeout(() => {
          this.rendered = false
        }, 3000)
      })
    }
  }
</script>

<style scoped>
  .notification-dialog {
    opacity: 0.9;
    width: 100%;
    height: 40px;
    z-index: 100;
    position: fixed;
    margin-top: 56px;
    border-radius: 20px;
  }
</style>
