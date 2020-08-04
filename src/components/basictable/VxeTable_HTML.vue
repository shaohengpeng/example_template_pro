<template>
  <vxe-table
          border
          :data="tableData">
          <vxe-table-column type="seq" width="60"></vxe-table-column>
          <vxe-table-column field="name" title="Name" sortable></vxe-table-column>
          <vxe-table-column field="describe" type="html" title="HTML 标签"></vxe-table-column>
          <vxe-table-column
            field="describeHtml"
            title="HTML 标签与筛选"
            type="html"
            sortable
            :filters="[{label:'包含 aa', value: 'aa'}, {label:'包含 bb', value: 'bb'}]"
            :filter-method="filterDescribeMethod"
            :sort-method="sortDescribeMethod"></vxe-table-column>
          <vxe-table-column field="role" type="html" title="HTML 标签与格式化" :formatter="formatRole"></vxe-table-column>
        </vxe-table>
</template>
<script>
export default {
          data () {
            return {
              tableData: [
                { name: 'xx1', describe: '字母 aa -1', describeHtml: '<span style="color: red">字母 <span style="color: blue">aa</span> -1</span>', role: 'oo1' },
                { name: 'xx2', describe: '字母 bb -2', describeHtml: '<span style="color: blue">字母 <span style="color: green">bb</span> -2</span>', role: 'oo2' },
                { name: 'xx3', describe: '字母 cc -3', describeHtml: '<span style="color: green">字母 <span style="color: red">cc</span> -3</span>', role: 'oo3' },
                { name: 'xx4', describe: '字母 dd -4', describeHtml: '<span style="color: blue">字母 <span style="color: green">dd</span> -4</span>', role: 'oo4' }
              ]
            }
          },
          methods: {
            formatRole ({ cellValue }) {
              return `<a href="https://github.com/x-extends/vxe-table" class="link" target="_black" style="color: orange">链接 ${cellValue}</a>`
            },
            sortDescribeMethod (a, b) {
              // 由于 HTML 是无法排序的，使用自定义排序
              var v1 = a.describe
              var v2 = b.describe
              return v1 < v2 ? -1 : v1 > v2 ? 1 : 0
            },
            filterDescribeMethod ({ value, row, column }) {
              return XEUtils.toString(row.html1).indexOf(value) > -1
            }
          }
        }
</script>