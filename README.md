# elementplus-table-encapsulation

elementplus-table-encapsulation，基于element-plus的el-table的二次封装使用demo

## Usage

```vue
<template>
  <div>
    <EncapTable
      :tableData="tableData"
      :height="500"
      :defaultSort="defaultSort"
      :pageData="pageData"
      :config="tableConfig"
      emptyText="暂无数据"
      stripe
      border
      @select="handleMultiSelect"
      @rowClick="handleRowClick"
      @dbClick="handleRowDbClick"
      @search="handleSearch"
      @operate="handleOperate"
    />
  </div>
</template>

<script setup lang="ts">
import { onMounted, reactive, ref } from 'vue'
import axios from 'axios'
import EncapTable from '@/components/EncapTable/EncapTable.vue';

const tableData = ref([])
const defaultSort = reactive({
  prop: 'date',
  order: 'descending'
})
const pageData = reactive({
  pageNo: 1,
  pageSize: 15,
  total: 0,
  sizesArr: [15, 30, 50, 100],
  position: 'center'
})

const tableConfig = ref([
  {
    type: 'selection',
    width: 65,
    align: 'center',
    fixed: 'left'
  },
  {
    type: 'index',
    label: '序号',
    width: 65,
    align: 'center',
    fixed: 'left'
  },
  {
    type: 'data',
    align: 'center',
    label: '名称',
    prop: 'name',
    searchable: true,
    searchType: 'input'
  },
  {
    type: 'data',
    align: 'center',
    label: '头像',
    prop: 'thumb',
    slot: 'image'
  },
  {
    type: 'data',
    align: 'center',
    label: '金额',
    prop: 'money',
    searchable: true,
    searchType: 'input',
    slot: 'text',
    slotContent: '￥'
  },
  {
    type: 'data',
    align: 'center',
    label: '日期',
    prop: 'date',
    searchable: true,
    searchType: 'time',
    timeType: 'date',
    valueFormat: 'YYYY-MM-DD',
    width: 200,
    minWidth: 200
  },
  {
    type: 'data',
    align: 'center',
    label: '地址',
    prop: 'address',
    searchType: 'input',
    searchable: true,
    minWidth: 250
  },
  {
    type: 'data',
    align: 'center',
    label: '状态',
    prop: 'state',
    searchable: true,
    searchType: 'select',
    options: [
      { label: '成功', value: true },
      { label: '失败', value: false }
    ],
    width: 100,
    slot: 'tag',
    tagType: (row: any, item: any) => { return row[item.prop] == '失败' ? 'danger' : 'success' }
  },
  {
    type: 'operation',
    align: 'center',
    label: '操作',
    width: 200,
    fixed: 'right',
    buttons: [
      {
        event: 'edit',
        type: 'primary',
        icon: 'EditPen',
        text: '编辑',
        size: 'small',
        controll: (row: any) => { return false }
      },
      {
        event: 'delete',
        type: 'danger',
        icon: 'Delete',
        text: '删除',
        size: 'small',
        controll: (row: any) => { return false }
      }
    ]
  }
])

onMounted(() => {
  getData()
})

const getData = () => {
  axios.post('https://www.fastmock.site/mock/2b34a823b8b83582c5da93412b0ca649/api/randomList').then(res => {
    console.log(res.data)
    tableData.value = res.data.data.list
    pageData.total = res.data.data.total
  }).catch(e => {
    console.log(e)
  })
}

const handleMultiSelect = (data: any) => {
  console.log('MultiSelect data => ', data)
}

const handleRowClick = (data: any) => {
  console.log('rowCLick data => ', data)
}
const handleRowDbClick = (data: any) => {
  console.log('rowDbCLick data => ', data)
}
const handleSearch = (data: any) => {
  console.log('search info => ', data)
}
const handleOperate = (type: string, data: any) => {
  console.log('operate =>', type, data)
}
</script>

```




## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin) to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension
   1) Run `Extensions: Show Built-in Extensions` from VSCode's command palette
   2) Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`
2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```