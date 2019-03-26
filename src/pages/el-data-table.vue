<template>
  <div>
    <el-data-table
      totalPath="total_count"
      dataPath="items"
      :url="url"
      :columns="columns"
      :searchForm="searchForm"
      :hasEdit="false"
      :extraButtons="extraButtons"
      :operationAttrs="operationAttrs"
    ></el-data-table>
  </div>
</template>

<script>
import ElDataTable from 'el-data-table'
import {formatDate} from '../const/filter'

export default {
  components: {
    'el-data-table': ElDataTable
  },
  data() {
    return {
      url: '/el-data-table/api/v1/component',
      columns: [
        {type: 'selection'},
        {prop: 'name', label: '组件名称'},
        {prop: 'type', label: '分类'},
        {prop: 'version', label: '版本'},
        {prop: 'language', label: '开发语言'},
        {
          prop: 'updateTime',
          label: '最后更新时间',
          formatter: row => {
            return formatDate(row.updateTime, 'YYYY-MM-DD')
          }
        },
        {
          prop: 'status',
          label: '状态',
          formatter: row => {
            if (row.status) {
              return <span style="color:green">上架</span>
            } else {
              return <span>下架</span>
            }
          }
        }
      ],
      searchForm: [
        {
          $el: {placeholder: '请输入', 'suffix-icon': 'el-icon-edit-outline'},
          label: '组件名称',
          $id: 'name',
          $type: 'input'
        },
        {
          $el: {placeholder: '请选择'},
          label: '分类',
          $id: 'type',
          $type: 'select'
        },
        {
          $el: {placeholder: '请选择'},
          label: '状态',
          $id: 'status',
          $type: 'select',
          $options: [{label: '上架', value: 1}, {label: '下架', value: 0}]
        }
      ],
      extraButtons: [
        {
          type: 'primary',
          size: 'mini',
          text: '查看',
          atClick: () => {
            return Promise.resolve()
          }
        },
        {
          text: '编辑',
          atClick: () => {
            return Promise.resolve()
          }
        },
        {
          text: '上架',
          atClick: () => {
            return Promise.resolve()
          },
          show: row => {
            return !row.status
          }
        },
        {
          text: '下架',
          atClick: () => {
            return Promise.resolve()
          },
          show: row => {
            return row.status
          }
        }
      ],
      operationAttrs: {
        minWidth: '100'
      }
    }
  }
}
</script>
