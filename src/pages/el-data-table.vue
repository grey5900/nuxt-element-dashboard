<template>
  <div class="data-table">
    <el-data-table v-bind="tableConfig"></el-data-table>
  </div>
</template>

<script>
import {mapState} from 'vuex'

const _categoryOptions = [
  '前端组件',
  '测试子组件',
  '分布式工具',
  '应用服务',
  '数据存储'
]

const _statusOptions = [
  {value: true, label: '上架'},
  {value: false, label: '下架'}
]

export default {
  data() {
    return {
      tableConfig: {
        url: '/deepexi-permission/api/v1/tables',
        hasView: false,
        hasDelete: false,
        hasSelect: true,
        single: false,
        paginationSize: 20,
        headerButtons: [
          {
            type: 'danger', 
            text: '删除', 
            disabled: selected => selected.length == 0,
            atClick: selected => {
              let ids = selected.map(v => v.id)

            }
          }
        ],
        extraButtons: [
          {
            type: 'primary',
            text: '查看',
            atClick: row => Promise.resolve()
          },
          {
            type: '',
            text: '下架',
            atClick: row => Promise.resolve()
          }
        ],
        hasEdit: true,
        columns: [
          {
            type: 'selection',
            width: '30'
          },
          {
            prop: 'name',
            label: '组件名称',
            width: '120'
          },
          {
            prop: 'category',
            label: '分类',
            width: '100',
            formatter: row => _categoryOptions[row.category - 1]
          },
          {
            prop: 'version',
            label: '版本',
            width: '150'
          },
          {
            prop: 'language',
            label: '开发语言',
            width: '150'
          },
          {
            prop: 'updateTime',
            label: '最后更新时间'
          },
          {
            prop: 'status',
            label: '状态',
            width: '100',
            formatter: row => row.status ? <span style="color: #8bc34a">上架</span> : '下架'
          }
        ],
        searchForm: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            $el: {
              placeholder: '请输入'
            }
          },
          {
            $type: 'select',
            $id: 'category',
            label: '分类',
            $options: _categoryOptions.map(i => ({value: i, label: _categoryOptions[i - 1]}))
          },
          {
            $type: 'select',
            $id: 'status',
            label: '状态 ',
            $options: _statusOptions.map(item => item)
          }
        ],
        form: [
          {
            $type: 'input',
            $id: 'name',
            label: '组件名称',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '组件名称',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'select',
            $id: 'category',
            label: '分类',
            $el: {
              placeholder: '请选择'
            },
            $options: _categoryOptions.map(i => ({value: i, label: _categoryOptions[i - 1]})),
            rules: [
              {
                required: true,
                message: '请选择类别',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'language',
            label: '开发语言',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '填写开发语言',
                trigger: 'blur'
              }
            ]
          },
          {
            $type: 'input',
            $id: 'version',
            label: '版本',
            $el: {
              placeholder: '请输入'
            },
            rules: [
              {
                required: true,
                message: '填写版本',
                trigger: 'blur'
              }
            ]
          }
        ]
      }
    }
  },
  created() {},
  methods: {},
  fetch({store, params}) {
    return store.dispatch('fetchDataTableList')
  },
  computed: {
    ...mapState(['list'])
  }
}
</script>
<style lang="less">
.table {
}
</style>
