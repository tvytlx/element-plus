## Checkbox

Un grupo de opciones para manejar múltiples elecciones.

### Uso básico

Checkbox puede ser usado para alternar entre dos estados.

:::demo Define `v-model`(enlaza la variable) en `el-checkbox`. El valor por defecto es un `Boolean` para un `checkbox`, y se convierte en `true` cuando este es seleccionado. El contenido dentro del tag `el-checkbox` se convierte en la descripción al costado del botón del checkbox.

```html
<template>
  <div>
    <el-checkbox v-model="checked1" label="Option 1"></el-checkbox>
    <el-checkbox v-model="checked2" label="Option 2"></el-checkbox>
  </div>
  <div>
    <el-checkbox
      v-model="checked3"
      label="Option 1"
      size="medium"
    ></el-checkbox>
    <el-checkbox
      v-model="checked4"
      label="Option 2"
      size="medium"
    ></el-checkbox>
  </div>
  <div>
    <el-checkbox v-model="checked5" label="Option 1" size="small"></el-checkbox>
    <el-checkbox v-model="checked6" label="Option 2" size="small"></el-checkbox>
  </div>
  <div>
    <el-checkbox v-model="checked7" label="Option 1" size="mini"></el-checkbox>
    <el-checkbox v-model="checked8" label="Option 2" size="mini"></el-checkbox>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        checked1: true,
        checked2: false,
        checked3: false,
        checked4: false,
        checked5: false,
        checked6: false,
        checked7: false,
        checked8: false,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      const checked1 = ref(true);
      const checked2 = ref(false);
      const checked3 = ref(false);
      const checked4 = ref(false);
      const checked5 = ref(false);
      const checked6 = ref(false);
      const checked7 = ref(false);
      const checked8 = ref(false);
      return {
        checked1,
        checked2,
        checked3,
        checked4,
        checked5,
        checked6,
        checked7,
        checked8,
      };
    },
  });

</setup>
-->
```

:::

### Estado Deshabilitado

Estado deshabilitado para el checkbox.

:::demo Setear el atributo `disabled`.

```html
<template>
  <el-checkbox v-model="checked1" disabled>Opción</el-checkbox>
  <el-checkbox v-model="checked2" disabled>Opción</el-checkbox>
</template>
<script>
  export default {
    data() {
      return {
        checked1: false,
        checked2: true,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      const checked1 = ref(false);
      const checked2 = ref(true);
      return {
        checked1,
        checked2,
      };
    },
  });
</setup>
-->
```

:::

### Grupo de Checkboxes

Es usado por múltiples checkboxes los cuales están enlazados a un grupo, indica si una opción está seleccionada verificando si esta está marcada.

:::demo El elemento `checkbox-group` puede manejar múltiples checkboxes en un grupo usando `v-model` el cuál está enlazado a un `Array`. Dentro del elemento `el-checkbox`, `label` es el valor del checkbox. Si en ese tag no hay contenido anidado, `label` va a ser mostrado como la descripción al lado del botón del checkbox. `label` también se corresponde con los valores del array. Es seleccionado si el valor especificado existe en el array y viceversa.

```html
<template>
  <el-checkbox-group v-model="checkList">
    <el-checkbox label="Opción A"></el-checkbox>
    <el-checkbox label="Opción B"></el-checkbox>
    <el-checkbox label="Opción C"></el-checkbox>
    <el-checkbox label="disabled" disabled></el-checkbox>
    <el-checkbox label="Seleccionado y deshabilitado" disabled></el-checkbox>
  </el-checkbox-group>
</template>

<script>
  export default {
    data() {
      return {
        checkList: ['Seleccionado y deshabilitado', 'Opción A'],
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, ref } from 'vue';

  export default defineComponent({
    setup() {
      const checkList = ref(['Seleccionado y deshabilitado','Opción A']);
      return {
        checkList,
      };
    },
  });

</setup>
-->
```

:::

### Indeterminado

La propiedad `indeterminate` puede ser usada para generar el efecto de marcar todos (check all).

:::demo

```html
<template>
  <el-checkbox
    :indeterminate="isIndeterminate"
    v-model="checkAll"
    @change="handleCheckAllChange"
    >Marcar todos</el-checkbox
  >
  <el-checkbox-group
    v-model="checkedCities"
    @change="handleCheckedCitiesChange"
  >
    <el-checkbox v-for="city in cities" :label="city" :key="city"
      >{{city}}</el-checkbox
    >
  </el-checkbox-group>
</template>
<script>
  const cityOptions = ['Shanghai', 'Beijing', 'Guangzhou', 'Shenzhen']
  export default {
    data() {
      return {
        checkAll: false,
        checkedCities: ['Shanghai', 'Beijing'],
        cities: cityOptions,
        isIndeterminate: true,
      }
    },
    methods: {
      handleCheckAllChange(val) {
        this.checkedCities = val ? cityOptions : []
        this.isIndeterminate = false
      },
      handleCheckedCitiesChange(value) {
        let checkedCount = value.length
        this.checkAll = checkedCount === this.cities.length
        this.isIndeterminate =
          checkedCount > 0 && checkedCount < this.cities.length
      },
    },
  }
</script>
<!--
<setup>

  import { defineComponent, reactive, toRefs } from 'vue';

  const cityOptions = ['Shanghai', 'Beijing', 'Guangzhou', 'Shenzhen'];

  export default defineComponent({
    setup() {
      const state = reactive({
        checkAll: false,
        checkedCities: ['Shanghai', 'Beijing'],
        cities: cityOptions,
        isIndeterminate: true,
      });
      const handleCheckAllChange = (val) => {
        state.checkedCities = val ? cityOptions : [];
        state.isIndeterminate = false;
      };
      const handleCheckedCitiesChange = (value) => {
        const checkedCount = value.length;
        state.checkAll = checkedCount === state.cities.length;
        state.isIndeterminate = checkedCount > 0 && checkedCount < state.cities.length;
      };
      return {
        ...toRefs(state),
        handleCheckAllChange,
        handleCheckedCitiesChange,
      };
    },
  });

</setup>
-->
```

:::

### Cantidad Mínima / Máxima de elementos seleccionados

Las propiedades `min` y `max` pueden limitar la cantidad de elementos seleccionados.

:::demo

```html
<template>
  <el-checkbox-group v-model="checkedCities" :min="1" :max="2">
    <el-checkbox v-for="city in cities" :label="city" :key="city"
      >{{city}}</el-checkbox
    >
  </el-checkbox-group>
</template>
<script>
  const cityOptions = ['Shanghai', 'Beijing', 'Guangzhou', 'Shenzhen']
  export default {
    data() {
      return {
        checkedCities: ['Shanghai', 'Beijing'],
        cities: cityOptions,
      }
    },
  }
</script>
<!--
<setup>

  import { defineComponent, reactive, toRefs } from 'vue';

  const cityOptions = ['Shanghai', 'Beijing', 'Guangzhou', 'Shenzhen'];

  export default defineComponent({
    setup() {
      const state = reactive({
        checkedCities: ['Shanghai', 'Beijing'],
        cities: cityOptions,
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

### Estilo tipo Botón

Checkbox con estilo tipo Botón.

:::demo Sólo debe cambiar el elemento `el-checkbox` por el elemento `el-checkbox-button`. También proveemos el atributo `size`.

```html
<template>
  <div>
    <el-checkbox-group v-model="checkboxGroup1">
      <el-checkbox-button v-for="city in cities" :label="city" :key="city"
        >{{city}}</el-checkbox-button
      >
    </el-checkbox-group>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup2" size="medium">
      <el-checkbox-button v-for="city in cities" :label="city" :key="city"
        >{{city}}</el-checkbox-button
      >
    </el-checkbox-group>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup3" size="small">
      <el-checkbox-button
        v-for="city in cities"
        :label="city"
        :disabled="city === 'Beijing'"
        :key="city"
        >{{city}}</el-checkbox-button
      >
    </el-checkbox-group>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup4" size="mini" disabled>
      <el-checkbox-button v-for="city in cities" :label="city" :key="city"
        >{{city}}</el-checkbox-button
      >
    </el-checkbox-group>
  </div>
</template>
<script>
  const cityOptions = ['Shanghai', 'Beijing', 'Guangzhou', 'Shenzhen']

  export default {
    data() {
      return {
        checkboxGroup1: ['Shanghai'],
        checkboxGroup2: ['Shanghai'],
        checkboxGroup3: ['Shanghai'],
        checkboxGroup4: ['Shanghai'],
        cities: cityOptions,
      }
    },
  }
</script>
<!--
<setup>

import { defineComponent, reactive, toRefs } from 'vue';

const cityOptions = ['Shanghai', 'Beijing', 'Guangzhou', 'Shenzhen'];

export default defineComponent({
  setup() {
    const state = reactive({
      checkboxGroup1: ['Shanghai'],
      checkboxGroup2: ['Shanghai'],
      checkboxGroup3: ['Shanghai'],
      checkboxGroup4: ['Shanghai'],
      cities: cityOptions,
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

### Con bordes

:::demo El atributo `border` agrega un borde a los Checkboxes.

```html
<template>
  <div>
    <el-checkbox v-model="checked1" label="Opción1" border></el-checkbox>
    <el-checkbox v-model="checked2" label="Opción2" border></el-checkbox>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox
      v-model="checked3"
      label="Opción1"
      border
      size="medium"
    ></el-checkbox>
    <el-checkbox
      v-model="checked4"
      label="Opción2"
      border
      size="medium"
    ></el-checkbox>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup1" size="small">
      <el-checkbox label="Opción1" border></el-checkbox>
      <el-checkbox label="Opción2" border disabled></el-checkbox>
    </el-checkbox-group>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup2" size="mini" disabled>
      <el-checkbox label="Opción1" border></el-checkbox>
      <el-checkbox label="Opción2" border></el-checkbox>
    </el-checkbox-group>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        checked1: true,
        checked2: false,
        checked3: false,
        checked4: true,
        checkboxGroup1: [],
        checkboxGroup2: [],
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
        checked1: true,
        checked2: false,
        checked3: false,
        checked4: true,
        checkboxGroup1: [],
        checkboxGroup2: [],
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

### Atributos de Checkbox

| Atributo              | Descripción                                                      | Tipo                               | Valores aceptados     | Por defecto |
| --------------------- | ---------------------------------------------------------------- | ---------------------------------- | --------------------- | ----------- |
| model-value / v-model | valor enlazado                                                   | string / number / boolean          | —                     | —           |
| label                 | valor del Checkbox si es usado dentro de un tag `checkbox-group` | string / number / boolean / object | —                     | —           |
| true-label            | valor del Checkbox si está marcado                               | string / number                    | —                     | —           |
| false-label           | valor del Checkbox si no está marcado                            | string / number                    | —                     | —           |
| disabled              | especifica si el Checkbox está deshabilitado                     | boolean                            | —                     | false       |
| border                | especifica si agrega un borde alrededor del Checkbox             | boolean                            | —                     | false       |
| size                  | tamaño del Checkbox                                              | string                             | medium / small / mini | —           |
| name                  | atributo `name` nativo                                           | string                             | —                     | —           |
| checked               | especifica si el Checkbox está marcado                           | boolean                            | —                     | false       |
| indeterminate         | similar a `indeterminate` en el checkbox nativo                  | boolean                            | —                     | false       |

### Eventos de Checkbox

| Nombre | Descripción                                | Parametros           |
| ------ | ------------------------------------------ | -------------------- |
| change | se ejecuta cuando el valor enlazado cambia | el valor actualizado |

### Atributos de Checkbox-group

| Atributo              | Descripción                                                | Tipo    | Valores aceptados     | Por Defecto |
| --------------------- | ---------------------------------------------------------- | ------- | --------------------- | ----------- |
| model-value / v-model | valor enlazado                                             | array   | —                     | —           |
| size                  | size of checkbox                                           | string  | medium / small / mini | —           |
| disabled              | especifica si los checkboxes anidados están deshabilitados | boolean | —                     | false       |
| min                   | cantidad mínima de checkboxes que deben ser marcados       | number  | —                     | —           |
| max                   | cantidad máxima de checkboxes que pueden ser marcados      | number  | —                     | —           |
| text-color            | color de fuente cuando el botón está activo                | string  | —                     | #ffffff     |
| fill                  | color de border y de fondo cuando el botón está activo     | string  | —                     | #409EFF     |

### Eventos de Checkbox-group

| Nombre de Evento | Descripción                                | Parametros           |
| ---------------- | ------------------------------------------ | -------------------- |
| change           | se ejecuta cuando el valor enlazado cambia | el valor actualizado |

### Atributos de Checkbox-button

| Atributo    | Descripción                                                      | Tipo                               | Valores aceptados | Por defecto |
| ----------- | ---------------------------------------------------------------- | ---------------------------------- | ----------------- | ----------- |
| label       | valor del checkbox cuando es usado dentro de un `checkbox-group` | string / number / boolean / object | —                 | —           |
| true-label  | valor del checkbox si este está marcado                          | string / number                    | —                 | —           |
| false-label | valor del checkbox si este no está marcado                       | string / number                    | —                 | —           |
| disabled    | especifica si el checkbox está deshabilitado                     | boolean                            | —                 | false       |
| name        | atributo 'name' del checbox nativo                               | string                             | —                 | —           |
| checked     | si el checkbox está marcado                                      | boolean                            | —                 | false       |
