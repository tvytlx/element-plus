## Pagination 分页

当数据量过多时，使用分页分解数据。

### 基础用法

:::demo 设置`layout`，表示需要显示的内容，用逗号分隔，布局元素会依次显示。`prev`表示上一页，`next`为下一页，`pager`表示页码列表，除此以外还提供了`jumper`和`total`，`size`和特殊的布局符号`->`，`->`后的元素会靠右显示，`jumper`表示跳页元素，`total`表示总条目数，`size`用于设置每页显示的页码数量。

```html
<template>
  <div class="block">
    <span class="demonstration">页数较少时的效果</span>
    <el-pagination layout="prev, pager, next" :total="50"> </el-pagination>
  </div>
  <div class="block">
    <span class="demonstration">大于 7 页时的效果</span>
    <el-pagination layout="prev, pager, next" :total="1000"> </el-pagination>
  </div>
</template>
```

:::

### 设置最大页码按钮数

:::demo 默认情况下，当总页数超过 7 页时，Pagination 会折叠多余的页码按钮。通过`pager-count`属性可以设置最大页码按钮数。

```html
<template>
  <el-pagination
    :page-size="20"
    :pager-count="11"
    layout="prev, pager, next"
    :total="1000"
  >
  </el-pagination>
</template>
```

:::

### 带有背景色的分页

:::demo 设置`background`属性可以为分页按钮添加背景色。

```html
<template>
  <el-pagination background layout="prev, pager, next" :total="1000">
  </el-pagination>
</template>
```

:::

### 小型分页

在空间有限的情况下，可以使用简单的小型分页。

:::demo 只需要一个`small`属性，它接受一个`Boolean`，默认为`false`，设为`true`即可启用。

```html
<template>
  <el-pagination small layout="prev, pager, next" :total="50"> </el-pagination>
</template>
```

:::

### 附加功能

根据场景需要，可以添加其他功能模块。

:::demo 此例是一个完整的用例，使用了`size-change`和`current-change`事件来处理页码大小和当前页变动时候触发的事件。`page-sizes`接受一个整型数组，数组元素为展示的选择每页显示个数的选项，`[100, 200, 300, 400]`表示四个选项，每页显示 100 个，200 个，300 个或者 400 个。

```html
<template>
  <div class="block">
    <span class="demonstration">显示总数</span>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      v-model:currentPage="currentPage1"
      :page-size="100"
      layout="total, prev, pager, next"
      :total="1000"
    >
    </el-pagination>
  </div>
  <div class="block">
    <span class="demonstration">调整每页显示条数</span>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      v-model:currentPage="currentPage2"
      :page-sizes="[100, 200, 300, 400]"
      :page-size="100"
      layout="sizes, prev, pager, next"
      :total="1000"
    >
    </el-pagination>
  </div>
  <div class="block">
    <span class="demonstration">直接前往</span>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      v-model:currentPage="currentPage3"
      :page-size="100"
      layout="prev, pager, next, jumper"
      :total="1000"
    >
    </el-pagination>
  </div>
  <div class="block">
    <span class="demonstration">完整功能</span>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage4"
      :page-sizes="[100, 200, 300, 400]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="400"
    >
    </el-pagination>
  </div>
</template>
<script>
  export default {
    methods: {
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`)
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`)
      },
    },
    data() {
      return {
        currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      const handleSizeChange = (val) => {
        console.log(`每页 ${val} 条`);
      };
      const handleCurrentChange = (val) => {
        console.log(`当前页: ${val}`);
      };

      return {
        currentPage1: ref(5),
        currentPage2: ref(5),
        currentPage3: ref(5),
        currentPage4: ref(4),
        handleSizeChange,
        handleCurrentChange,
      };
    },
  });

</setup>
-->
```

:::

### 当只有一页时隐藏分页

当只有一页时，通过设置 `hide-on-single-page` 属性来隐藏分页。

:::demo

```html
<template>
  <div>
    <el-switch v-model="value"> </el-switch>
    <el-pagination
      :hide-on-single-page="value"
      :total="5"
      layout="prev, pager, next"
    >
    </el-pagination>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        value: false,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      return {
        value: ref(false),
      };
    },
  });

</setup>
-->
```

:::

### Attributes

| 参数                 | 说明                                                                                                                  | 类型     | 可选值                                                            | 默认值                                 |
| -------------------- | --------------------------------------------------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------- | -------------------------------------- |
| small                | 是否使用小型分页样式                                                                                                  | boolean  | —                                                                 | false                                  |
| background           | 是否为分页按钮添加背景色                                                                                              | boolean  | —                                                                 | false                                  |
| page-size            | 每页显示条目个数，支持 v-model 双向绑定                                                                               | number   | —                                                                 | 10                                     |
| default-page-size    | 每页显示条目数的初始值；                                                                                              | number   | -                                                                 | -                                      |
| total                | 总条目数                                                                                                              | number   | —                                                                 | —                                      |
| page-count           | 总页数，total 和 page-count 设置任意一个就可以达到显示页码的功能；如果要支持 page-sizes 的更改，则需要使用 total 属性 | Number   | —                                                                 | —                                      |
| pager-count          | 页码按钮的数量，当总页数超过该值时会折叠                                                                              | number   | 大于等于 5 且小于等于 21 的奇数                                   | 7                                      |
| current-page         | 当前页数，支持 v-model 双向绑定                                                                                       | number   | —                                                                 | 1                                      |
| default-current-page | 当前页数的初始值                                                                                                      | number   | -                                                                 | -                                      |
| layout               | 组件布局，子组件名用逗号分隔                                                                                          | String   | `sizes`, `prev`, `pager`, `next`, `jumper`, `->`, `total`, `slot` | 'prev, pager, next, jumper, ->, total' |
| page-sizes           | 每页显示个数选择器的选项设置                                                                                          | number[] | —                                                                 | [10, 20, 30, 40, 50, 100]              |
| popper-class         | 每页显示个数选择器的下拉框类名                                                                                        | string   | —                                                                 | —                                      |
| prev-text            | 替代图标显示的上一页文字                                                                                              | string   | —                                                                 | —                                      |
| next-text            | 替代图标显示的下一页文字                                                                                              | string   | —                                                                 | —                                      |
| disabled             | 是否禁用                                                                                                              | boolean  | —                                                                 | false                                  |
| hide-on-single-page  | 只有一页时是否隐藏                                                                                                    | boolean  | —                                                                 | -                                      |

:::warning
我们现在会检查一些不合理的用法，如果发现分页器未显示，可以核对是否违反以下情形：

- `total` 和 `page-count` 必须传一个，不然组件无法判断总页数；优先使用 `page-count`;
- 如果传入了 `current-page` 必须监听 `current-page` 变更的事件（`onUpdate:currentPage`）；否则分页切换不起作用；
- 如果传入了 `page-size`，且布局包含 `page-size` 选择器（即 `layout` 包含 `sizes`），必须监听 `page-size` 变更的事件（`onUpdate:pageSize`），否则 `page-size` 切换不起作用；
  :::

### Events

| 事件名称       | 说明                               | 回调参数 |
| -------------- | ---------------------------------- | -------- |
| size-change    | pageSize 改变时会触发              | 每页条数 |
| current-change | currentPage 改变时会触发           | 当前页   |
| prev-click     | 用户点击上一页按钮改变当前页后触发 | 当前页   |
| next-click     | 用户点击下一页按钮改变当前页后触发 | 当前页   |

:::warning
以上事件不推荐使用；如果要监听 current-page 和 page-size 的改变，使用 v-model 双向绑定是个更好的选择。
:::

### Slot

| name | 说明                                      |
| ---- | ----------------------------------------- |
| —    | 自定义内容，需要在 `layout` 中列出 `slot` |
