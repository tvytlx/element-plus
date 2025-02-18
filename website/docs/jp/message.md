## メッセージ

アクティビティ後のフィードバックを表示するために使用されます。Notification との違いは、後者はシステムレベルの受動的な通知を表示するために使用されることが多いことです。

### 基本的な使い方

上部に表示され、3 秒後に消えます。

:::demo メッセージの設定は通知と非常に似ているので、ここではオプションの詳細については説明しません。以下のオプション表と notification のドキュメントを組み合わせて確認すると理解が深まります。要素には `$message` メソッドを登録しています。メッセージは文字列か VNode をパラメータに取ることができ、それが本文として表示されます。

```html
<template>
  <el-button :plain="true" @click="open">Show message</el-button>
  <el-button :plain="true" @click="openVn">VNode</el-button>
</template>

<script>
  import { h } from 'vue'

  export default {
    methods: {
      open() {
        this.$message('This is a message.')
      },

      openVn() {
        this.$message({
          message: h('p', null, [
            h('span', null, 'Message can be '),
            h('i', { style: 'color: teal' }, 'VNode'),
          ]),
        })
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent, h } from 'vue';
  import { ElMessage } from 'element-plus';

  export default defineComponent({
    setup() {
      
      const open = () => {
        ElMessage('this is a message.');
      };

      const openVn = () => {
        ElMessage({
          message: h('p', null, [
            h('span', null, 'Message can be '),
            h('i', { style: 'color: teal' }, 'VNode'),
          ]),
        });
      };

      return {
        open,
        openVn,
      };
    },
  });

</setup>
-->
```

:::

### タイプ

成功、警告、メッセージ、エラーのアクティビティのフィードバックを表示するために使用されます。

:::demo さらにカスタマイズが必要な場合は、メッセージコンポーネントはオブジェクトをパラメータとして受け取ることもできます。例えば、`type`の値を設定することで異なるタイプを定義することができ、デフォルトは `info` です。このような場合、`message`の値として本体が渡されます。また、型ごとにメソッドを登録しているので、`open4`のように型を渡さずに直接呼び出すこともできる。

```html
<template>
  <el-button :plain="true" @click="open2">success</el-button>
  <el-button :plain="true" @click="open3">warning</el-button>
  <el-button :plain="true" @click="open1">message</el-button>
  <el-button :plain="true" @click="open4">error</el-button>
</template>

<script>
  export default {
    methods: {
      open1() {
        this.$message('This is a message.')
      },
      open2() {
        this.$message({
          message: 'Congrats, this is a success message.',
          type: 'success',
        })
      },

      open3() {
        this.$message({
          message: 'Warning, this is a warning message.',
          type: 'warning',
        })
      },

      open4() {
        this.$message.error('Oops, this is a error message.')
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent } from 'vue';
  import { ElMessage } from 'element-plus';

  export default defineComponent({
    setup() {
      
      const open1 = () => {
        ElMessage('this is a message.');
      };
      const open2 = () => {
        ElMessage({
          message: 'Congrats, this is a success message.',
          type: 'success',
        });
      };
      const open3 = () => {
        ElMessage({
          message: 'Warning, this is a warning message.',
          type: 'warning',
        });
      };
      const open4 = () => {
        ElMessage.error('Oops, this is a error message.');
      };
      return {
        open1,
        open2,
        open3,
        open4,
      };
    },
  });

</setup>
-->
```

:::

### クローズ可能

閉じるボタンを追加することができます。

:::demo デフォルトのメッセージは手動で閉じることができません。メッセージを閉じたい場合は `showClose` フィールドを設定することができます。通知と同様に、メッセージにも制御可能な `duration` があります。デフォルトの持続時間は 3000ms で、`0`に設定してもメッセージは消えません。

```html
<template>
  <el-button :plain="true" @click="open1">message</el-button>
  <el-button :plain="true" @click="open2">success</el-button>
  <el-button :plain="true" @click="open3">warning</el-button>
  <el-button :plain="true" @click="open4">error</el-button>
</template>

<script>
  export default {
    methods: {
      open1() {
        this.$message({
          showClose: true,
          message: 'This is a message.',
        })
      },

      open2() {
        this.$message({
          showClose: true,
          message: 'Congrats, this is a success message.',
          type: 'success',
        })
      },

      open3() {
        this.$message({
          showClose: true,
          message: 'Warning, this is a warning message.',
          type: 'warning',
        })
      },

      open4() {
        this.$message({
          showClose: true,
          message: 'Oops, this is a error message.',
          type: 'error',
        })
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent } from 'vue';
  import { ElMessage } from 'element-plus';

  export default defineComponent({
    setup() {
      
      const open1 = () => {
        ElMessage({
          showClose: true,
          message: 'This is a message.',
        });
      };
      const open2 = () => {
        ElMessage({
          showClose: true,
          message: 'Congrats, this is a success message.',
          type: 'success',
        });
      };
      const open3 = () => {
        ElMessage({
          showClose: true,
          message: 'Warning, this is a warning message.',
          type: 'warning',
        });
      };
      const open4 = () => {
        ElMessage({
          showClose: true,
          message: 'Oops, this is a error message.',
          type: 'error',
        });
      };
      return {
        open1,
        open2,
        open3,
        open4,
      };
    },
  });

</setup>
-->
```

:::

### 中央のテキスト

テキストを中央に配置するには `center` 属性を使用します。

:::demo

```html
<template>
  <el-button :plain="true" @click="openCenter">Centered text</el-button>
</template>

<script>
  export default {
    methods: {
      openCenter() {
        this.$message({
          message: 'Centered text',
          center: true,
        })
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent } from 'vue';
  import { ElMessage } from 'element-plus';

  export default defineComponent({
    setup() {
      
      const openCenter = () => {
        ElMessage({
          showClose: true,
          message: 'Centered text',
        });
      };
      return {
        openCenter,
      };
    },
  });

</setup>
-->
```

:::

### HTML 文字列を使用します。

`message` は HTML 文字列をサポートしています。

:::demo `dangerouslyUseHTMLString` を true に設定すると、`message` は HTML 文字列として扱われます。

```html
<template>
  <el-button :plain="true" @click="openHTML">Use HTML String</el-button>
</template>

<script>
  export default {
    methods: {
      openHTML() {
        this.$message({
          dangerouslyUseHTMLString: true,
          message: '<strong>This is <i>HTML</i> string</strong>',
        })
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent } from 'vue';
  import { ElMessage } from 'element-plus';

  export default defineComponent({
    setup() {
      
      const openCenter = () => {
        ElMessage({
          dangerouslyUseHTMLString: true,
          message: '<strong>This is <i>HTML</i> string</strong>',
        });
      };
      return {
        openCenter,
      };
    },
  });

</setup>
-->
```

:::

:::warning
`message`プロパティは HTML 文字列をサポートしていますが、任意の HTML を動的にレンダリングすると[XSS 攻撃](https://en.wikipedia.org/wiki/Cross-site_scripting)につながりやすく、非常に危険です。したがって、`dangerouslyUseHTMLString`がオンの場合は、`message`の内容が信頼できるものであることを確認し、**決して**ユーザが提供したコンテンツに`message`を代入しないようにしてください。
:::

### グローバルメソッド

要素には、Vue.prototype 用のグローバルメソッド `$message` が追加されました。これにより、vue のインスタンスでは、このページで行ったように `Message` を呼び出すことができます。

### ローカルインポート

```javascript
import { ElMessage } from 'element-plus'
```

この場合は `ElMessage(options)` を呼び出す必要があります。また、`ElMessage.success(options)`のように、異なるタイプのメソッドも登録しています。すべてのインスタンスを手動で閉じるには、`ElMessage.closeAll()`を呼び出すことができます。

### オプション

| Attribute                | Description                                                            | Type           | Accepted Values            | Default |
| ------------------------ | ---------------------------------------------------------------------- | -------------- | -------------------------- | ------- |
| message                  | メッセージテキスト                                                     | string / VNode | —                          | —       |
| type                     | メッセージタイプ                                                       | string         | success/warning/info/error | info    |
| iconClass                | カスタムアイコンのクラス、 `type` をオーバーライドします。             | string         | —                          | —       |
| dangerouslyUseHTMLString | `message` を HTML 文字列として扱うかどうか                             | boolean        | —                          | false   |
| customClass              | メッセージ用カスタムクラス名                                           | string         | —                          | —       |
| duration                 | 表示時間、ミリ秒。0 に設定した場合、自動的にはオフになりません。       | number         | —                          | 3000    |
| showClose                | 閉じるボタンを表示するかどうか                                         | boolean        | —                          | false   |
| center                   | テキストを中央に配置するかどうか                                       | boolean        | —                          | false   |
| onClose                  | メッセージのインスタンスをパラメータにして閉じた場合のコールバック関数 | function       | —                          | —       |
| offset                   | ビューポートの上端までの距離を設定します                               | number         | —                          | 20      |

### メソッド

`Message` と `this.$message` は現在の Message インスタンスを返します。インスタンスを手動で閉じるには、そのインスタンスに対して `close` を呼び出すことができます。
| Method | Description |
| ---- | ---- |
| close | メッセージを閉じる |
