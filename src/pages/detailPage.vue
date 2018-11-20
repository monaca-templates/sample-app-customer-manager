<template>
  <v-content class="detail-container">
    <Header>
      <v-btn icon class="header-icon" slot="navi" @click="backToList"><v-icon>arrow_back</v-icon></v-btn>
      <template slot="title">{{ $t('detail.title') }}</template>
      <HeaderMenu
        slot="menus"
        @on-click-edit="goToUpdate"
        @on-click-delete="deleteCustomer"
      ></HeaderMenu>
    </Header>
    <v-card>
      <Detail :customer="customer"></Detail>
    </v-card>
  </v-content>
</template>

<script>
  import Detail from '../components/detail/Detail'
  import Header from '../components/header/Header'
  import HeaderMenu from '../components/detail/HeaderMenu'
  import { EventBus } from '../eventBus.js'

  export default {
    name: 'DetailPage',
    components: {
      Header,
      HeaderMenu,
      Detail,
    },
    props: {
      id: String,
      customer: Object,
    },
    data: () => {
      return {
        menuModal: false,
      }
    },
    methods: {
      deleteCustomer () {
        // データベースアクセス
        firebase.database().ref(`customer_list/${this.id}`)
          .remove()
        EventBus.$emit('notify', this.$t('notify.deleted_customer'), 'success')
        this.backToList()
      },
      goToUpdate () {
        this.$router.push({
          name: 'update',
          params: { id: this.id, customer: this.customer }
        })
      },
      backToList () {
        this.$router.push({
          name: 'list'
        })
      }
    }
  }
</script>

<style>
  .detail-container {
    padding: 82px 26px 0px 26px !important;
  }
</style>
