<template>
  <v-list-tile
    @click="$emit('on-click-list-item', id, customer)"
    class="list-item"
  >
    <div class="border-wrapper">
      <v-list-tile-content>
        <v-list-tile-title>{{ customer.company }}</v-list-tile-title>
        <v-list-tile-sub-title>{{ $t('list.staff', { staff: customer.staff }) }}</v-list-tile-sub-title>
      </v-list-tile-content>
    </div>
  </v-list-tile>
</template>

<script>
  export default {
    name: 'ListItem',
    props: {
      id: String,
      customer: Object,
    }
  }
</script>

<style scoped>
.border-wrapper {
  width: 90%;
  height: 100%;
  margin: 0 5% 0 5%;
  border-bottom: #dddddd 1px solid;
}
</style>
