<template>
  <v-content class="detail-container">
    <Header>
      <v-btn icon slot="navi" class="header-icon" @click="backToList">
        <v-icon>arrow_back</v-icon>
      </v-btn>
      <template slot="title">{{ $t('create.title') }}</template>
      <template slot="menus"></template>
    </Header>
    <v-card>
      <Edit
        :customer="customer"
        @on-edit-customer="editCustomer"
      ></Edit>
      <EditButtons
        @complete="completeEdit"
        @cancel="backToList"
      ></EditButtons>
    </v-card>
  </v-content>
</template>

<script>
  import Edit from '../components/edit/Edit'
  import Header from '../components/header/Header'
  import EditButtons from '../components/edit/EditButtons'
  import { EventBus } from '../eventBus.js'

  export default {
    name: 'CreatePage',
    components: {
      Header,
      Edit,
      EditButtons,
    },
    data: () => {
      return {
        customer: {}
      }
    },
    methods: {
      editCustomer (key, val) {
        this.customer[key] = val
      },
      completeEdit () {
        if (!this.checkRequire()) return
        // チェックをパスした場合データベースを更新して画面遷移
        this.setNewCustomer()
        EventBus.$emit('notify', this.$t('notify.added_customer'), 'success')
        this.goToDetail()
      },
      goToDetail () {
        this.$router.push({
          name: 'detail',
          params: { customer: this.customer }
        })
      },
      backToList () {
        this.$router.push({
          name: 'list',
        })
      },
      // 必須項目チェック
      checkRequire () {
        const validatedList = []
        if (!this.customer.company) {
          validatedList.push(this.$t('customer.company'))
        }
        if (!this.customer.staff) {
          validatedList.push(this.$t('customer.staff'))
        }
        if (validatedList.length !== 0) {
          // チェックに引っかかったものからメッセージを作成して警告ダイアログを表示
          let require = ''
          for (let str of validatedList) {
            require += `「${str}」`
          }
          EventBus.$emit('notify', this.$t('notify.require_error', { require: require }), 'error')
          return false
        } else {
          return true
        }
      },
      setNewCustomer () {
        // データベースアクセス
        firebase.database().ref('customer_list').push(this.customer)
      }
    }
  }
</script>
