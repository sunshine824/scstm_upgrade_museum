<template>
  <div class="main">
    <div class="main-box clearfix">
      <div class="notice-list">
        <titles :titles="titles"></titles>
        <ul-group :data="lists ? lists : []" url="/paper"></ul-group>
        <Pagination
          v-if="lists[0]"
          :total="lists[0].page*10"
          :page="page"
          @handleChange="handlePage">
        </Pagination>
      </div>
    </div>
  </div>
</template>

<script>
  import titles from '@/base/title'
  import ulGroup from '@/base/ulGroup'
  import Pagination from '@/base/pagination'
  import {LIMIT} from '@/public/js/config'
  import {
    getPaperLists
  } from '@/public/js/api'

  export default {
    name: "paper",
    components: {
      titles,
      ulGroup,
      Pagination
    },
    data() {
      return {
        titles: {
          ch: '论文及成果',
          en: 'Papers and achievements',
        },
        page: 1,
        limit: LIMIT,
        lists: []
      }
    },
    created() {
      this._getPaperLists()
    },
    methods: {
      _getPaperLists: async function () {
        let result = await getPaperLists({
          page: this.page,
          limit: this.limit
        })
        this.lists = result.msg
      },
      handlePage(page) {
        this.page = page
        this._getPaperLists()
      }
    }
  }
</script>

<style scoped lang="less">
  .main {
    width: 100%;
    border: 1px solid #f5f3f0;
    .main-box {
      width: 100%;
      .main-list {
        float: left;
        width: 730px;
      }
      .dynamic {
        float: right;
        width: 424px;
        .title {
          margin-top: 0;
        }
      }
    }
  }
</style>
