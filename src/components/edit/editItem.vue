<template>
  <v-list-tile>
    <v-list-tile-action>
      <v-icon>{{ icon }}</v-icon>
    </v-list-tile-action>
    <v-list-tile-content>
      <v-text-field
        style="width:100%"
        :label="label"
        :value="customerValue"
        @input="editCustomer"
      ></v-text-field>
    </v-list-tile-content>
  </v-list-tile>
</template>

<script>
  export default {
    name: 'EditItem',
    props: {
      icon: String,
      label: String,
      customerKey: String,
      customerValue: String,
    },
    methods: {
      editCustomer (val) {
        this.$emit('on-edit-customer', this.customerKey, val)
      }
    }
  }
</script>
