<template>
  <div>
    <el-table
      v-loading="loading"
      v-bind="$attrs"
      :data="tableData"
      style="width: 100%"
      v-on="$listeners"
    >
      <slot />
    </el-table>
    <el-pagination class="pagination" :current-page.sync="queryOptions.current" :page-size.sync="queryOptions.size" layout="total, sizes, prev, pager, next, jumper" :total="total" @size-change="loadData" @current-change="loadData" />
  </div>

</template>

<script>
const initQueryOptions = () => {
  return {
    current: 1,
    size: 10
  }
}
export default {
  name: 'CTable',
  props: {
    query: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      loading: false,
      total: 0,
      queryOptions: initQueryOptions(),
      tableData: []
    }
  },
  created() {
    this.loadData()
  },
  methods: {
    async loadData() {
      this.loading = true
      const { data, total } = await this.query(this.queryOptions)
      this.total = total
      this.tableData = data
      this.loading = false
    },
    reload() {
      this.queryOptions = initQueryOptions()
      this.loadData()
    }
  }
}
</script>
