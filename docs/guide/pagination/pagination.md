<script setup>
import PaginationDefaultExample from './examples/PaginationDefaultExample.vue'
import PaginationLayoutExample from './examples/PaginationLayoutExample.vue'
import PaginationIconExample from './examples/PaginationIconExample.vue'
</script>
# Pagination

reference: [https://flowbite.com/docs/components/pagination/](https://flowbite.com/docs/components/pagination/)

## Basic example

<PaginationDefaultExample />

```vue
<script setup>
import { Pagination } from 'flowbite-vue'
</script>
<template>
  <Pagination></Pagination>
</template>
```

## Prop - layout

```typescript
type Layout = 'navigation' | 'pagination' | 'table'

defineProps({
    size: {
        type: String as PropType<Layout>,
        default: 'pagination',
    },
})
```

<PaginationLayoutExample />


```vue
<script setup>
import { Pagination } from 'flowbite-vue'
</script>
<template>
  <div class="vp-raw flex flex-col">
    <div class="mt-10 mb-4">Pagination</div>
    <Pagination layout="pagination" />
    <div class="mt-10 mb-4">Navigation</div>
    <Pagination layout="navigation" />
    <div class="mt-10 mb-4 mx-auto">Table</div>
    <Pagination layout="table" />
  </div>
</template
```

## Prop - showIcon

<PaginationIconExample />

```vue
<script setup>
import { Pagination } from 'flowbite-vue'
</script>
<template>
  <div class="vp-raw flex flex-col">
    <div class="mt-10 mb-4">Pagination</div>
    <Pagination showIcon layout="pagination" />
    <div class="mt-10 mb-4">Navigation</div>
    <Pagination showIcon layout="navigation" />
    <div class="mt-10 mb-4 mx-auto">Table</div>
    <Pagination showIcon layout="table" />
  </div>
</template
```
