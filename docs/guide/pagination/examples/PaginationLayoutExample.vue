<template>
  <div class="vp-raw flex flex-col">
    <div class="mt-10 mb-4">Pagination</div>
    <Pagination layout="pagination" :current="current" @page-change="current = $event"  />
    <div class="mt-10 mb-4">Navigation</div>
    <Pagination layout="navigation" :current="current" @page-change="current = $event"  />
    <div class="mt-10 mb-4 mx-auto">Table</div>
    <Pagination layout="table" :current="current" @page-change="current = $event" :total="100" />
  </div>
</template>
<script setup>
import { Pagination } from '../../../../src/index'
import { ref } from 'vue'
const current = ref(3)
</script>
