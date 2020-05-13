<template>
<div id="app">
  <Pagination 
    :data="data"
    :pagesize="2"
    :pagerange="5"
    @page-data="getPageData"
    @change-page="getPage"
  />

  <p>page {{ page }}</p>
  <p>pageData {{ pageData }}</p>
</div>
</template>

<script>
import Pagination from '@/components/Pagination.vue'

export default {
  name: 'App',
  components: {
    Pagination
  },
  data() {
    return {
      page: 1,
      pageData: [],
      data: [
        { id: '01' },
        { id: '02' },
        { id: '03' },
        { id: '04' },
        { id: '05' },
        { id: '06' },
        { id: '07' },
        { id: '08' },
        { id: '09' },
        { id: '10' },
        { id: '11' },
        { id: '12' },
        { id: '13' },
        { id: '14' },
        { id: '15' },
        { id: '16' },
        { id: '17' },
        { id: '18' },
        { id: '19' },
        { id: '20' },
        { id: '21' },
        { id: '22' },
        { id: '23' },
        { id: '24' },
        { id: '25' },
      ]
    }
  },
  methods: {
    getPageData(pageData) {
      this.pageData = pageData
    },
    getPage(page) {
      this.page = page
    }
  }
}
</script>

<style lang="scss">

</style>
