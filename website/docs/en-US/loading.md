## Loading

Show animation while loading data.

### Loading inside a container

Displays animation in a container (such as a table) while loading data.

:::demo Element Plus provides two ways to invoke Loading: directive and service. For the custom directive `v-loading`, you just need to bind a `boolean` value to it. By default, the loading mask will append to the element where the directive is used. Adding the `body` modifier makes the mask append to the body element.

```html
<template>
  <el-table v-loading="loading" :data="tableData" style="width: 100%">
    <el-table-column prop="date" label="Date" width="180"> </el-table-column>
    <el-table-column prop="name" label="Name" width="180"> </el-table-column>
    <el-table-column prop="address" label="Address"> </el-table-column>
  </el-table>
</template>

<style>
  body {
    margin: 0;
  }
</style>

<script>
  export default {
    data() {
      return {
        tableData: [
          {
            date: '2016-05-02',
            name: 'John Smith',
            address: 'No.1518,  Jinshajiang Road, Putuo District',
          },
          {
            date: '2016-05-04',
            name: 'John Smith',
            address: 'No.1518,  Jinshajiang Road, Putuo District',
          },
          {
            date: '2016-05-01',
            name: 'John Smith',
            address: 'No.1518,  Jinshajiang Road, Putuo District',
          },
        ],
        loading: true,
      }
    },
  }
</script>
<!--
<setup>

import { defineComponent, reactive, toRefs } from 'vue';

export default defineComponent({
  setup() {
    const state = reactive({
      tableData: [
        {
          date: '2016-05-02',
          name: 'John Smith',
          address: 'No.1518,  Jinshajiang Road, Putuo District',
        },
        {
          date: '2016-05-04',
          name: 'John Smith',
          address: 'No.1518,  Jinshajiang Road, Putuo District',
        },
        {
          date: '2016-05-01',
          name: 'John Smith',
          address: 'No.1518,  Jinshajiang Road, Putuo District',
        },
      ],
      loading: true,
    });
    return {
      ...toRefs(state),
    };
  },
});

</setup>
-->
```

:::

### Customization

You can customize loading text, loading spinner and background color.

:::demo Add attribute `element-loading-text` to the element on which `v-loading` is bound, and its value will be displayed under the spinner. Similarly, the `element-loading-spinner`, `element-loading-background`, and `element-loading-svg` attributes are used to set the icon class name, background color value, and loading icon, respectively.

```html
<template>
  <el-table
    v-loading="loading"
    element-loading-text="Loading..."
    element-loading-spinner="el-icon-loading"
    element-loading-background="rgba(0, 0, 0, 0.8)"
    :data="tableData"
    style="width: 100%"
  >
    <el-table-column prop="date" label="Date" width="180"> </el-table-column>
    <el-table-column prop="name" label="Name" width="180"> </el-table-column>
    <el-table-column prop="address" label="Address"> </el-table-column>
  </el-table>
  <el-table
    v-loading="loading"
    :element-loading-svg="svg"
    class="custom-loading-svg"
    element-loading-svg-view-box="-10, -10, 50, 50"
    :data="tableData"
    style="width: 100%"
  >
    <el-table-column prop="date" label="Date" width="180"> </el-table-column>
    <el-table-column prop="name" label="Name" width="180"> </el-table-column>
    <el-table-column prop="address" label="Address"> </el-table-column>
  </el-table>
</template>

<script>
  export default {
    data() {
      return {
        tableData: [
          {
            date: '2016-05-02',
            name: 'John Smith',
            address: 'No.1518,  Jinshajiang Road, Putuo District',
          },
          {
            date: '2016-05-04',
            name: 'John Smith',
            address: 'No.1518,  Jinshajiang Road, Putuo District',
          },
          {
            date: '2016-05-01',
            name: 'John Smith',
            address: 'No.1518,  Jinshajiang Road, Putuo District',
          },
        ],
        loading: true,
        svg: `
          <path class="path" d="
            M 30 15
            L 28 17
            M 25.61 25.61
            A 15 15, 0, 0, 1, 15 30
            A 15 15, 0, 1, 1, 27.99 7.5
            L 15 15
          " style="stroke-width: 4px; fill: rgba(0, 0, 0, 0)"/>
        `,
      }
    },
  }
</script>
<!--
<setup>

import { defineComponent, reactive, toRefs } from 'vue';

export default defineComponent({
  setup() {
    const state = reactive({
      tableData: [
        {
          date: '2016-05-02',
          name: 'John Smith',
          address: 'No.1518,  Jinshajiang Road, Putuo District',
        },
        {
          date: '2016-05-04',
          name: 'John Smith',
          address: 'No.1518,  Jinshajiang Road, Putuo District',
        },
        {
          date: '2016-05-01',
          name: 'John Smith',
          address: 'No.1518,  Jinshajiang Road, Putuo District',
        },
      ],
      loading: true,
      svg: `
        <path class="path" d="
          M 30 15
          L 28 17
          M 25.61 25.61
          A 15 15, 0, 0, 1, 15 30
          A 15 15, 0, 1, 1, 27.99 7.5
          L 15 15
        " style="stroke-width: 4px; fill: rgba(0, 0, 0, 0)"/>
      `,
    });
    return {
      ...toRefs(state),
    };
  },
});

</setup>
-->
```

:::

:::warning
Although the `element-loading-svg` attribute supports incoming HTML fragments, it is very dangerous to dynamically render arbitrary HTML on the website, because it is easy to cause [XSS attack](https://en.wikipedia.org/wiki/Cross-site_scripting). Please make sure that the content of `element-loading-svg` is trustworthy. **Never** assign user-submitted content to the `element-loading-svg` attribute.
:::

### Full screen loading

Show a full screen animation while loading data.

:::demo When used as a directive, a full screen Loading requires the `fullscreen` modifier, and it will be appended to body. In this case, if you wish to disable scrolling on body, you can add another modifier `lock`. When used as a service, Loading will be full screen by default.

```html
<template>
  <el-button
    type="primary"
    @click="openFullScreen1"
    v-loading.fullscreen.lock="fullscreenLoading"
  >
    As a directive
  </el-button>
  <el-button type="primary" @click="openFullScreen2"> As a service </el-button>
</template>

<script>
  export default {
    data() {
      return {
        fullscreenLoading: false,
      }
    },
    methods: {
      openFullScreen1() {
        this.fullscreenLoading = true
        setTimeout(() => {
          this.fullscreenLoading = false
        }, 2000)
      },
      openFullScreen2() {
        const loading = this.$loading({
          lock: true,
          text: 'Loading',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)',
        })
        setTimeout(() => {
          loading.close()
        }, 2000)
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';
  import { ElLoading } from 'element-plus';

  export default defineComponent({
    setup() {
      const fullscreenLoading = ref(false);
      const openFullScreen1 = () => {
        fullscreenLoading.value = true;
        setTimeout(() => {
          fullscreenLoading.value = false;
        }, 2000);
      };

      const openFullScreen2 = () => {
        const loading = ElLoading.service({
          lock: true,
          text: 'Loading',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)',
        });
        setTimeout(() => {
          loading.close();
        }, 2000);
      };

      return {
        fullscreenLoading,
        openFullScreen1,
        openFullScreen2,
      };
    },
  });

</setup>
-->
```

:::

### Service

You can also invoke Loading with a service. Import Loading service:

```javascript
import { ElLoading } from 'element-plus'
```

Invoke it:

```javascript
ElLoading.service(options)
```

The parameter `options` is the configuration of Loading, and its details can be found in the following table. `LoadingService` returns a Loading instance, and you can close it by invoking its `close` method:

```javascript
let loadingInstance = ElLoading.service(options)
this.$nextTick(() => {
  // Loading should be closed asynchronously
  loadingInstance.close()
})
```

Note that in this case the full screen Loading is singleton. If a new full screen Loading is invoked before an existing one is closed, the existing full screen Loading instance will be returned instead of actually creating another Loading instance:

```javascript
let loadingInstance1 = ElLoading.service({ fullscreen: true })
let loadingInstance2 = ElLoading.service({ fullscreen: true })
console.log(loadingInstance1 === loadingInstance2) // true
```

Calling the `close` method on any one of them can close this full screen Loading.

If Element Plus is imported entirely, a globally method `$loading` will be registered to `app.config.globalProperties`. You can invoke it like this: `this.$loading(options)`, and it also returns a Loading instance.

### Options

| Attribute   | Description                                                                                                                                                              | Type          | Accepted Values | Default       |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | --------------- | ------------- |
| target      | the DOM node Loading needs to cover. Accepts a DOM object or a string. If it's a string, it will be passed to `document.querySelector` to get the corresponding DOM node | object/string | —               | document.body |
| body        | same as the `body` modifier of `v-loading`                                                                                                                               | boolean       | —               | false         |
| fullscreen  | same as the `fullscreen` modifier of `v-loading`                                                                                                                         | boolean       | —               | true          |
| lock        | same as the `lock` modifier of `v-loading`                                                                                                                               | boolean       | —               | false         |
| text        | loading text that displays under the spinner                                                                                                                             | string        | —               | —             |
| spinner     | class name of the custom spinner                                                                                                                                         | string        | —               | —             |
| background  | background color of the mask                                                                                                                                             | string        | —               | —             |
| customClass | custom class name for Loading                                                                                                                                            | string        | —               | —             |

### Directives

| Name                       | Description                                  | Type    |
| -------------------------- | -------------------------------------------- | ------- |
| v-loading                  | show animation while loading data            | boolean |
| element-loading-text       | loading text that displays under the spinner | string  |
| element-loading-spinner    | class name of the custom spinner             | string  |
| element-loading-background | background color of the mask                 | string  |
