<template>
  <v-list two-line>
    <v-slide-y-transition class="py-0" group  tag="v-list">
      <ListItem
        v-for="(item, key, index) in customerList"
        v-if="isCurrentPageContent(index)"
        :key="key"
        :id="key"
        :customer="item"
        @on-click-list-item="goToDetail"
      ></ListItem>
    </v-slide-y-transition>
  </v-list>
</template>

<script>
  import ListItem from './listItem'

  export default {
    name: 'List',
    components: {
      ListItem
    },
    props: {
      currentPage: Number,
      customerList: Object,
      rows: Number,
    },
    methods: {
      goToDetail (id, customer) {
        this.$router.push({
          name: 'detail',
          params: { id: id, customer: customer }
        })
      },
      isCurrentPageContent (index) {
        // 現在のページに表示するコンテンツかどうかを判定する
        return ((this.currentPage - 1) * this.rows < index + 1) && (index + 1 <= this.currentPage * this.rows)
      }
    }
  }
</script>

