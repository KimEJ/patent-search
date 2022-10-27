<template>
  <div class="search">
    <h1>search result</h1>
    {{data}}
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Search',
  data() {
    return { 
      data: ''
    }
  },

  mounted() {
    axios.get("http://lod.kipo.kr/data/search/endpoint", {
      params: {
        searchKeyword: this.$route.query.token,
        contextStr: 'patent',
        currentPage: 1,
        displayNum: 10,
        requestType: 'HTML'
      }
    }, {
      withCredentials: true
    }).then((response) => {
      console.log(response)
      this.data = response
    })
  }

}
</script>

<style>
@media (min-width: 1024px) {
  .search {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
