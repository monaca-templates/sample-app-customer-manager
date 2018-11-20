<template>
  <v-list two-line>
    <EditItem
      :icon="'domain'"
      :label="$t('customer.company')"
      :customer-key="'company'"
      :customer-value="customer.company"
      @on-edit-customer="editCustomer"
    ></EditItem>
    <EditItem
      :icon="'person'"
      :label="$t('customer.staff')"
      :customer-key="'staff'"
      :customer-value="customer.staff"
      @on-edit-customer="editCustomer"
    ></EditItem>
    <EditItem
      :icon="'phone'"
      :label="$t('customer.TEL')"
      :customer-key="'TEL'"
      :customer-value="customer.TEL"
      @on-edit-customer="editCustomer"
    ></EditItem>
    <EditItem
      :icon="'mail'"
      :label="$t('customer.email')"
      :customer-key="'email'"
      :customer-value="customer.email"
      @on-edit-customer="editCustomer"
    ></EditItem>
    <EditItem
      :icon="'place'"
      :label="$t('customer.address')"
      :customer-key="'address'"
      :customer-value="customer.address"
      @on-edit-customer="editCustomer"
    ></EditItem>
  </v-list>
</template>

<script>
  import EditItem from './editItem'

  export default {
    name: 'Edit',
    components: {
      EditItem
    },
    props: {
      customer: Object
    },
    methods: {
      editCustomer (key, val) {
        this.$emit('on-edit-customer', key, val)
      }
    },
  }
</script>
