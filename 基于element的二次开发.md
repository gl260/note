# i-el-table 组件

```vue
<template>
  <div class="i-el-table">
    <el-table class="un-empty-image-table" :data="data" size="medium" :header-cell-style="{ background: '#f5f7fa' }">
      <!-- 添加空数据插槽 -->
      <template v-if="showEmpty" slot="empty">
        <el-empty :description="emptyText"></el-empty>
      </template>

      <template v-for="(v, i) in tableTitle">
        <!-- 有多级表头 -->
        <el-table-column
          v-if="v.children && v.children.length && checkColumnCondition(v)"
          :key="i"
          :label="v.label"
          :align="v.align || 'left'"
        >
          <template v-for="(child, j) in v.children">
            <el-table-column
              v-if="checkColumnCondition(child)"
              :key="`${i}-${j}`"
              :label="child.label"
              :prop="child.prop"
              :align="child.align || 'left'"
              :width="child.width"
              :min-width="child.minWidth"
              :fixed="child.fixed"
            >
              <template v-slot="{ row }">
                <span style="white-space: pre-line">{{ formatColumnValue(row, child) }}</span>
              </template>
            </el-table-column>
          </template>
        </el-table-column>

        <!-- 操作列(插槽) -->
        <el-table-column
          v-else-if="v.slot && checkColumnCondition(v)"
          :key="i"
          :label="v.label"
          :align="v.align || 'left'"
          :width="v.width"
          :min-width="v.minWidth"
          :fixed="v.fixed"
        >
          <template v-slot="{ row }">
            <slot :name="v.slot" :row="row"></slot>
          </template>
        </el-table-column>

        <!-- 没有多级表头 -->
        <el-table-column
          v-else-if="checkColumnCondition(v)"
          :key="i"
          :label="v.label"
          :prop="v.prop"
          :align="v.align || 'left'"
          :width="v.width"
          :min-width="v.minWidth"
          :fixed="v.fixed"
        >
          <template v-slot="{ row }">
            <!-- <span>{{ row[v.prop] || 'N/A' }}</span> -->
            <span style="white-space: pre-line">{{ formatColumnValue(row, v) }}</span>
          </template>
        </el-table-column>
      </template>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'i-el-table',
  props: {
    tableData: { type: Array, default: () => [] },
    tableTitle: { type: Array, default: () => [] },
    showEmpty: { type: Boolean, default: false },
    emptyText: { type: String, default: 'No Data' },
  },
  data() {
    return {
      data: [],
    };
  },
  watch: {
    tableData: {
      handler(v) {
        this.data = v;
      },
    },
  },
  created() {},
  methods: {
    formatColumnValue(row, column) {
      if (column.formatter) {
        return column.formatter(row[column.prop], row);
      } else {
        return row[column.prop] || 'N/A';
      }
    },
    // 检查列的条件是否满足
    checkColumnCondition(column) {
      // 如果没有设置condition，则默认显示
      if (!column.condition && column.condition !== false) {
        return true;
      }

      // 如果condition是函数，则执行函数判断
      if (typeof column.condition === 'function') {
        return column.condition();
      }

      // 如果condition是布尔值，则直接返回
      return !!column.condition;
    },
  },
};
</script>
```

## 组件概述

i-el-table 是一个基于 Element UI Table 二次封装的表格组件，提供了更简便的配置方式和更强大的功能，包括多级表头、列格式化、条件渲染列与自定义操作列等。

## 基本用法

```vue
<template>
  <i-el-table 
    :table-data="tableData" 
    :table-title="tableTitle"
    :show-empty="true"
    :empty-text="$t('NoData')"
  ></i-el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [], // 表格数据
      tableTitle: [
        { label: '名称', prop: 'name' },
        { label: '年龄', prop: 'age' }
      ]
    }
  }
}
</script>
```

## 组件属性

| 属性       | 类型    | 默认值    | 说明               |
| ---------- | ------- | --------- | ------------------ |
| tableData  | Array   | []        | 表格数据           |
| tableTitle | Array   | []        | 表格列配置         |
| showEmpty  | Boolean | false     | 是否显示空数据模板 |
| emptyText  | String  | 'No Data' | 空数据时显示的文本 |

## tableTitle 列配置项

列配置是通过 `tableTitle` 数组进行设置，每个元素代表一列，支持以下属性：

| 属性      | 类型             | 说明                                      |
| --------- | ---------------- | ----------------------------------------- |
| label     | String           | 列标题                                    |
| prop      | String           | 列属性名                                  |
| align     | String           | 列对齐方式，默认 'left'                   |
| width     | String/Number    | 列宽度                                    |
| minWidth  | String/Number    | 列最小宽度                                |
| fixed     | Boolean/String   | 列是否固定，可选值：true、'left'、'right' |
| formatter | Function         | 列格式化函数，参数为：(cellValue, row)    |
| slot      | String           | 自定义插槽名称，用于自定义列内容          |
| children  | Array            | 子列配置，用于多级表头                    |
| condition | Function/Boolean | 条件渲染函数或布尔值，决定是否显示该列    |

## 列格式化

通过 `formatter` 函数对列数据进行格式化：

```js
tableTitle: [
  {
    label: '状态',
    prop: 'status',
    formatter: (value, row) => {
      return ['禁用', '启用'][value] || 'N/A';
    }
  }
]
```

formatter 函数接收两个参数：
- `value`: 单元格的值
- `row`: 行数据对象

## 条件渲染列

使用 `condition` 属性可以根据条件决定是否显示某列：

```js
tableTitle: [
  {
    label: '特殊功能1',
    prop: 'special1',
    formatter: v => ['禁用', '启用'][v] || 'N/A',
    // 条件函数，返回布尔值决定是否显示该列
    condition: () => this.Flag == 1
  },
  {
    label: '特殊功能2',
    prop: 'special2',
    // 直接使用布尔值
    condition: false // 该列不会显示
  }
]
```

## 多级表头

通过 `children` 属性可以设置多级表头：

```js
tableTitle: [
  {
    label: '流量统计',
    align: 'center',
    children: [
      { label: '接收数据', prop: 'receive' },
      { label: '发送数据', prop: 'send' }
    ]
  }
]
```

## 自定义列内容

通过 `slot` 属性设置插槽名，可以自定义列内容：

```vue
<template>
  <i-el-table :table-data="tableData" :table-title="tableTitle">
    <!-- 使用命名插槽自定义操作列 -->
    <template #operation="{ row }">
      <el-button type="text" @click="editBtn(row)">
        编辑
      </el-button>
    </template>
  </i-el-table>
</template>

<script>
export default {
  data() {
    return {
      tableTitle: [
        { label: '姓名', prop: 'name' },
        { label: '操作', slot: 'operation', width: '90', fixed: 'right' }
      ]
    }
  },
  methods: {
    getPONEdit(row) {
      // 判断逻辑
    },
    editBtn(row) {
      // 编辑逻辑
    }
  }
}
</script>
```

## 空数据处理

设置 `showEmpty` 和 `emptyText` 属性可以自定义空数据时的显示：

```vue
<i-el-table
  :table-data="tableData"
  :table-title="tableTitle"
  :show-empty="true"
  :empty-text="$t('PortFig55')"
></i-el-table>
```



## 完整使用示例

```vue
<template>
  <div>
    <i-el-table
      :table-data="tableData"
      :table-title="tableTitle"
      :show-empty="true"
      :empty-text="空数据提示"
    >
      <template #operation="{ row }">
        <el-button type="text" @click="editBtn(row)">
          编辑
        </el-button>
      </template>
    </i-el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [],
      Model: null,
      tableTitle: [
        { label: '名称', prop: 'Name', width: 90, fixed: true },
        { 
          label: '开关', 
          prop: 'Switch',
          width: 110,
          formatter: v => ['开启', '关闭'][v] || 'N/A',
          condition: () => this.Flag == xxx
        },
        {
          label: '(pps)',
          align: 'center',
          children: [
            { label: '', prop: '' },
            { label: '', prop: '' },
            { label: '', prop: '' }
          ]
        },
        { label: '操作', slot: 'operation', fixed: 'right', width: '90' }
      ]
    }
  },
}
</script>
```

## 性能优化建议

1. **延迟加载大数据**：对于大量数据，考虑使用分页或虚拟滚动
2. **合理使用固定列**：过多的固定列会影响性能
3. **优化格式化函数**：避免在格式化函数中执行复杂计算
4. **提取公共格式化逻辑**：将常用的格式化函数封装到单独的工具文件中

---

通过合理配置 `tableTitle`，结合条件渲染和自定义插槽，可以快速创建功能丰富的表格，大大简化表格开发工作。



# i-el-Form组件

