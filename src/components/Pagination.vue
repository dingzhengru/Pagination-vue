<template>
<div class="pagination-div">
  
  <ul class="pagination">
    <li
      :class="{ 'disabled': page <= 1 }"
      @click="prevPage"
    >
      <a href="javascript:;">上頁</a>
    </li>

    <!-- 第一頁 -->
    <li :class="{'active-li': page == 1}" @click="changePage(1)">
      <a href="javascript:;">1</a>
    </li>
    <!-- 第一頁 -->

    <!-- 第...頁 -->
    <li class="disabled" v-show="isHideLeftPage">
      <a href="javascript:;">...</a>
    </li>
    <!-- 第...頁 -->

    <li 
      v-for="p in range(2, totalPage - 1)"
      :key="p"
      :class="{'active-li': page == p}"
      @click="changePage(p)"
      v-show="isShowPage(p)"

    >
      <a 
        href="javascript:;"
        v-show="isShowPage(p)"
      >{{ p }}</a>
    </li>

    <!-- 第...頁 -->
    <li class="disabled" v-show="isHideRightPage">
      <a href="javascript:;">...</a>
    </li>
    <!-- 第...頁 -->

    <!-- 最後一頁 (最後一頁 = 1 也是不顯示) -->
    <li :class="{'active-li': page == totalPage}" @click="changePage(totalPage)" v-if="totalPage != 1">
      <a href="javascript:;">{{ totalPage }}</a>
    </li>
    <!-- 最後一頁 -->

    <li 
      :class="{ 'disabled': page >= totalPage }"
      @click="nextPage"
    >
      <a href="javascript:;">下頁</a>
    </li>
  </ul>
</div>
</template>

<script>



export default {
  name: 'AppPagination',
  props: {
    data: {
      type: Array,
      default: () => []
    },
    startpage: {
      type: Number,
      default: () => 1
    },
    pagesize: {
      type: Number,
      default: () => 10
    },
    pagerange: { // 最多顯示頁數，需是奇數(偶數的話，看要 +1 或 -1 去調整)
      type: Number,
      default: () => 3
    }
  },
  data() {
    return {
      page: this.startpage,
      clonePageRange: this.pagerange
    }
  },
  computed: {
    pageData() {
      let startAt = this.pagesize * (this.page - 1)
      let endAt = startAt + this.pagesize
      return this.data.slice(startAt, endAt) || []
    },
    totalPage() {
      return Math.ceil(this.data.length / this.pagesize)
    },
    halfPageRange() { // 用來計算 pageRange 相關用的
      return Math.floor(this.clonePageRange / 2) // 無條件捨去
    },
    isHideLeftPage() {
      /*
        依照此規律，所以需要 halfPageRange
        1 => +-0
        3 => +-1
        5 => +-2
      */
      return this.page > (3 + this.halfPageRange)
    },
    isHideRightPage() {
      // return this.page < this.totalPage - 4
      // return this.page < this.totalPage - 3
      return this.page < (this.totalPage - 2 - this.halfPageRange)
    }
  },
  methods: {
    isShowPage(page) {

      // 左邊頁數已經到可以連接上的數量時
      // if((this.page < 5 && page < 5)) {
      //   return true
      // }

      if((this.page < (4 + this.halfPageRange) && page < (4 + this.halfPageRange))) {
        return true
      }

      // 右邊頁數已經到可以連接上的數量時
      // if(page > this.totalPage - 4 && this.page > this.totalPage - 4) {
      //   return true
      // }

      if(page > (this.totalPage - 3 - this.halfPageRange) && this.page > (this.totalPage - 3 - this.halfPageRange)) {
        return true
      }

      // 只顯示三頁 (page, page+1, page-1)
      // if(this.isHideLeftPage || this.isHideRightPage) {
      //   if(page > this.page + 1 || page < this.page - 1) {
      //     return false
      //   }
      // }

      if(this.isHideLeftPage || this.isHideRightPage) {
        if(page > this.page + this.halfPageRange || page < this.page - this.halfPageRange) {
          return false
        }
      }
      return true
    },
    prevPage() {
      if(this.page <= 1)
        return
      this.page--
    },
    nextPage() {
      if(this.page >= this.totalPage)
        return
      this.page++
    },
    changePage(page) {
      this.page = page
    },
    range(start, end, step = 1) {
      const len = Math.floor((end - start) / step) + 1
      if(len <= 0)
        return []
      return Array(len).fill().map((_, idx) => start + (idx * step))
    }
  },
  watch: {
    page: {
      immediate: true,
      handler() {
        this.$emit('page-data', this.pageData)
        this.$emit('change-page', this.page)
      }
    },
    data: {
      immediate: true,
      handler() {
        this.$emit('page-data', this.pageData)
      }
    },
    pagesize: {
      immediate: false,
      handler() {
        this.$emit('page-data', this.pageData)
      }
    },
    cloneVisiblePages: {
      immediate: true,
      handler(newVal) {
        if(newVal % 2 == 0) {
          this.cloneVisiblePages++
        }
      }
    }
  }
}
</script>

<style scoped>


</style>