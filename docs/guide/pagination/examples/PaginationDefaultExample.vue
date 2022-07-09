<template>
  <div class="vp-raw flex flex-col">
    <Pagination class="my-4" :current="current" @page-change="current = $event" />
    <Pagination class="my-4" :paginationItems="9" :current="current" @page-change="current = $event" />
    <Pagination class="my-4" :paginationItems="11" :current="current" @page-change="current = $event" />
  </div>
</template>
<script setup>
import { Pagination } from '../../../../src/index'
import { ref } from 'vue'
const current = ref(3)
</script>
