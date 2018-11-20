<template>
  <div>
    <v-btn icon class="header-icon" @click="$emit('on-click-search')">
      <v-icon>search</v-icon>
    </v-btn>
    <v-btn icon class="header-icon" @click="$emit('on-click-add')">
      <v-icon>add</v-icon>
    </v-btn>
  </div>
</template>

<script>
  export default {
    name: 'HeaderMenu',
  }
</script>
