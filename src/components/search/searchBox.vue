<template>
  <v-toolbar
    transition="slide-y-transition"
    class="search-box"
  >
    <v-text-field
      class="search-input"
      v-model="searchParam"
      hide-details
      prepend-icon="search"
      single-line
    ></v-text-field>
    <v-btn
      icon
      class="close-icon"
      @click="$emit('on-click-close')"
    >
      <v-icon>close</v-icon>
    </v-btn>
  </v-toolbar>
</template>

<script>
  export default {
    name: 'SearchBox',
    props: {
      customerListCopy: Object,
    },
    data: () => {
      return {
        searchParam: '',
      }
    },
    computed: {
      result () {
        let resultData = {}
        for (let id in this.customerListCopy) {
          for (let key in this.customerListCopy[id]) {
            if (this.customerListCopy[id][key].indexOf(this.searchParam) > -1) {
              // 検索文字列が部分一致したものを結果セットに入れて表示する
              resultData[id] = this.customerListCopy[id]
            }
          }
        }
        return resultData
      }
    },
    watch: {
      // 検索ボックスの入力を監視
      searchParam () {
        this.$emit('on-input', this.result)
      }
    },
  }
</script>

<style scoped>
  .search-box {
    width: 90%;
    margin: -12px 5% !important;
  }
  .close-icon {
    margin: 12px -16px 0 16px;
  }
</style>
