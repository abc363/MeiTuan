<template>
  <div class="i-table">

    <div class="table-container">
      <el-table
        border
        :data="tableData"
        @selection-change="handleSelectionChange">
        <el-table-column
          v-if="selectionShow"
          type="selection"
          width="55"
          align="center">
        </el-table-column>

        <slot></slot>
      </el-table>
    </div>

    <div class="table-pagination" v-show="tableData.length && paginationVisible">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="pageInfo.pageNum"
        :page-sizes="[5, 10, 20, 50, 100]"
        :page-size="pageInfo.pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="pageInfo.total">
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  name: 'i-table',
  props: {
    tableData: {
      type: Array,
      default: () => {
        return []
      }
    },
    pageInfo: {
      type: Object,
      default: () => {
        return {
          pageIndex: 1,
          pageSize: 5,
          total: 0
        }
      }
    },
    selectionShow: {
      type: Boolean,
      default: false
    },
    paginationVisible: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      currentPage: 1
    }
  },
  watch: {
    pageInfo (value) {
      console.log('value', value)
    }
  },
  methods: {
    // 每页条数
    handleSizeChange (value) {
      this.$emit('handleSizeChange', value)
    },
    // 当前页数
    handleCurrentChange (value) {
      this.$emit('handleCurrentChange', value)
    },
    // 多选框改变
    handleSelectionChange (rows) {
      this.$emit('selection-change', rows)
    }
  }
}
</script>

<style lang="less" scoped>
.i-table {
  padding: 10px;
  // .table-container{
  //   .el-table__header-wrapper{
  //     .has-gutter{
  //       tr{
  //         background-color: red;
  //       }
  //     }
  //   }
  // }
  .btn-list {
    margin-bottom: 10px;
  }

  .table-pagination {
    .el-pagination {
      text-align: right;
    }
  }
}
</style>
