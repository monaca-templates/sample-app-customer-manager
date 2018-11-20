<template>
  <v-list two-line>
    <v-list-tile>
      <v-list-tile-content>
    <h1 class="display-1">{{ customer.company }}</h1>
      </v-list-tile-content>
    </v-list-tile>
    <DetailItem
      :icon="'person'"
      :title="customer.staff"
      :subtitle="$t('customer.staff')"
    ></DetailItem>
    <DetailItem
      :icon="'phone'"
      :title="customer.TEL"
      :subtitle="$t('customer.TEL')"
    ></DetailItem>
    <DetailItem
      :icon="'mail'"
      :title="customer.email"
      :subtitle="$t('customer.email')"
    ></DetailItem>
    <DetailItem
      :icon="'place'"
      :title="customer.address"
      :subtitle="$t('customer.address')"
    ></DetailItem>
    <Map
      :address="customer.address"
    ></Map>
  </v-list>
</template>

<script>
  import DetailItem from './detailItem'
  import Map from '../map/Map'

  export default {
    name: 'Detail',
    components: {
      DetailItem,
      Map,
    },
    props: {
      customer: Object
    },
  }
</script>

<style scoped>
  #mapbox {
    border: gray 1px solid;
    margin: 0 8px;
    width: calc(100% -16px);
    height: 240px;
  }
</style>
