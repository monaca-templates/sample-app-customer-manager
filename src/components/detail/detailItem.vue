<template>
  <v-list-tile>
    <v-list-tile-action>
      <v-icon>{{ icon }}</v-icon>
    </v-list-tile-action>
    <v-list-tile-content>
      <v-list-tile-title>{{ title }}</v-list-tile-title>
      <v-list-tile-sub-title>{{ subtitle }}</v-list-tile-sub-title>
    </v-list-tile-content>
  </v-list-tile>
</template>

<script>
  export default {
    name: '',
    props: {
      icon: String,
      title: String,
      subtitle: String,
    }
  }

</script>
