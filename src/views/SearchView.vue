<template>
  <div class="search">
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
    let uri = window.location.search.substring(1); 
    let params = new URLSearchParams(uri);
    
    axios.get("https://cors-anywhere.herokuapp.com/http://lod.kipo.kr/data/search/endpoint", {
      params: {
        searchKeyword: params.get("token"),
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
