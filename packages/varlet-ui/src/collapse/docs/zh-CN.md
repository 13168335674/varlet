# 折叠面板

### 介绍

可以折叠/展开的内容区域。

### 基本使用

通过 `v-model` 控制展开的面板列表，`value` 为数组格式。

```html
<script setup>
import { ref } from 'vue'

const value = ref(['1'])

const changeHandle = (val) => {
  console.log(val)
}
</script>

<template>
  <var-collapse v-model="value" @change="changeHandle">
    <var-collapse-item title="标题" name="1">文本</var-collapse-item>
    <var-collapse-item title="标题" name="2">文本</var-collapse-item>
  </var-collapse>
</template>
```
### 隐藏边距

使用 `offset` 属性隐藏边距。

```html
<script setup>
import { ref } from 'vue'

const value = ref(['2'])
</script>

<template>
  <var-collapse v-model="value" :offset="false">
    <var-collapse-item title="标题" name="1">文本</var-collapse-item>
    <var-collapse-item title="标题" name="2">文本</var-collapse-item>
  </var-collapse>
</template>
```

### 手风琴模式

使用 `accordion` 属性开启手风琴模式，此时 `value` 为字符串。

```html
<script setup>
import { ref } from 'vue'

const value = ref('')
</script>

<template>
  <var-collapse v-model="value" accordion :offset="false">
    <var-collapse-item title="标题" name="1">文本</var-collapse-item>
    <var-collapse-item title="标题" name="2">文本</var-collapse-item>
  </var-collapse>
</template>
```

### 禁用

在 `collapse-item` 上使用 `disabled` 属性禁用当前面板。

```html
<script setup>
import { ref } from 'vue'

const value = ref([1])

const disabled = ref(false)  
</script>

<template>
  <var-space direction="column" :size="[8, 8]">
    <var-button @click="disabled = !disabled">
      {{ disabled ? '启用' : '禁用' }}
    </var-button>
    
    <var-collapse v-model="value">
      <var-collapse-item title="标题" :name="1" :disabled="disabled">
        文本
      </var-collapse-item>
      <var-collapse-item title="标题" :name="2" :disabled="disabled">
        文本
      </var-collapse-item>
    </var-collapse>
  </var-space>
</template>
```

### 自定义内容

```html
<script setup>
import { ref } from 'vue'

const value = ref(['1'])  
</script>

<template>
  <var-collapse v-model="value">
    <var-collapse-item title="这是标题" name="1" icon="account-circle">
      文本
    </var-collapse-item>
    <var-collapse-item name="2">
      <template #title>这是标题</template>
      <template #icon>^_^</template>
      这是内容
    </var-collapse-item>
  </var-collapse>
</template>
```

## API

### 属性

#### Collapse Props

| 参数 | 说明 | 类型 | 默认值 |
| ----- | -------------- | -------- | ---------- |
| `v-model` | 当前展开面板的 name | 手风琴模式： _string \| number_<br> 非手风琴模式：_string[] \| number[]_ | `-` |
| `accordion` | 是否开启手风琴模式 | _boolean_ | `false` |
| `offset` | 是否显示边距 | _boolean_ | `true` |

#### CollapseItem Props

| 参数 | 说明 | 类型 | 默认值 |
| ----- | -------------- | -------- | ---------- |
| `name` | 唯一标识符，默认为索引值 | _string \| number_| `index` |
| `title` | 面板标题 | _string \| number_| `-` |
| `icon` | icon 的名称 | _string_ | `chevron-down` |
| `disabled` | 是否禁用面板 | _boolean_ | `false` |

### 事件

#### Collapse Events

| 事件名 | 说明 | 回调参数 |
| ----- | -------------- | -------- |
| `change` | 切换面板时触发| `value: 类型与 v-model 绑定的值一致` |

### 插槽

#### Collapse Slots

| 名称 | 说明      | 参数 |
| ----- |---------| -------- |
| `default` | 折叠面板的内容 | `-` |

#### CollapseItem Slots

| 名称 | 说明 | 参数 |
| ----- | -------------- | -------- |
| `default` | 面板的内容 | `-` |
| `title` | 面板的标题 | `-` |
| `icon` | 自定义右侧 icon | `-` |

### 样式变量
以下为组件使用的 css 变量，可以使用 [StyleProvider 组件](#/zh-CN/style-provider) 进行样式定制

| 变量名 | 默认值 |
| --- | --- |
| `--collapse-background` | `#fff` |
| `--collapse-text-color` | `#232222` |
| `--collapse-header-font-size` | `var(--font-size-lg)` |
| `--collapse-header-padding` | `10px 12px` |
| `--collapse-content-font-size` | `var(--font-size-md)` |
| `--collapse-content-padding` | `0 12px 10px` |
| `--collapse-item-margin-top` | `16px` |
| `--collapse-disable-color` | `#bdbdbd` |
| `--collapse-border-top` | `thin solid rgba(0, 0, 0, 0.12)` |
