<template>
  <detail-con :data="detail ? detail : {}"></detail-con>
</template>

<script>
  import {getFlowDetail} from '@/public/js/api'
  import DetailCon from '@/base/detail'

  export default {
    name: "detail",
    components: {
      DetailCon
    },
    data() {
      return {
        detail: {}
      }
    },
    created() {
      this._getFlowDetail()
    },
    methods: {
      _getFlowDetail: async function () {
        let result = await getFlowDetail({
          id: this.$route.params.id
        })
        this.detail = result.msg
      }
    }
  }
</script>

<style scoped lang="less">

</style>
