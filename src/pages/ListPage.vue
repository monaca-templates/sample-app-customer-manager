<template>
  <v-content class="list-container">
    <Header>
      <template slot="title">{{ $t('list.title') }}</template>
      <template slot="menus">
        <HeaderMenu
          @on-click-search="search"
          @on-click-add="goToAdd"
        >
        </HeaderMenu>
      </template>
    </Header>
    <SearchBox
      v-show="searchBox"
      :customer-list-copy="customerListCopy"
      @on-input="setCustomerList"
      @on-click-close="search"
    ></SearchBox>
    <List
      :current-page="page"
      :customer-list="customerList"
      :rows="rows"
    ></List>
    <v-footer fixed>
      <v-flex xs12>
        <div class="text-xs-center">
          <v-pagination
            fixed
            color="teal"
            v-model="page"
            :length="pagerLength"
          ></v-pagination>
        </div>
      </v-flex>
    </v-footer>
  </v-content>
</template>

<script>
  import Header from '../components/header/Header'
  import HeaderMenu from '../components/list/HeaderMenu'
  import List from '../components/list/List'
  import SearchBox from '../components/search/SearchBox'

  export default {
    name: 'ListPage',
    components: {
      Header,
      HeaderMenu,
      List,
      SearchBox,
    },
    data: () => {
      return {
        customerList: {},
        customerListCopy: {},
        page: 1,
        searchBox: false,
        rows: 10,
      }
    },
    computed: {
      pagerLength () {
        const count = Object.keys(this.customerList).length
        if (!count) {
          // 表示するデータが存在しない場合
          return 1
        } else if (!(count % this.rows)) {
          // 表示行数ちょうどの場合
          return count / this.rows
        } else {
          // 表示行数ちょうどでない場合は次のページに繰越す
          return Math.floor(count / this.rows) + 1
        }
      }
    },
    methods: {
      goToAdd () {
        this.$router.push({
          name: 'create'
        })
      },
      search () {
        // 検索ボックスの表示・非表示
        this.searchBox = !this.searchBox
      },
      getCustomerList () {
        // データベースアクセス
        firebase.database().ref('/customer_list').on('value', (ss) => {
          if (ss.val()) {
            this.setCustomerList(ss.val())
            this.cloneCustomerList()
          }
        })
      },
      setCustomerList (customerList) {
        this.customerList = customerList
      },
      cloneCustomerList () {
        // 絞り込み検索のためのコピーを作成
        this.customerListCopy = JSON.parse(JSON.stringify(this.customerList))
      },
    },
    mounted () {
      this.getCustomerList()
    }
  }
</script>

<style>
  .list-container {
    padding-top: 56px !important;
    padding-bottom: 36px !important;
  }
</style>
