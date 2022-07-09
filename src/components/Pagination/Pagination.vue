<template>
  <nav aria-label="Page navigation example">

    <!-- Table Layout -->
    <template v-if="layout === 'table'">
      <div class="flex flex-col items-center">
        <!-- Help text -->
        <span class="text-sm text-gray-700 dark:text-gray-400">
            Showing 
            <span class="font-semibold text-gray-900 dark:text-white">
              {{ (current - 1) * perPage + 1 }}
            </span>
            to
            <span class="font-semibold text-gray-900 dark:text-white">
              {{ current * perPage }}
            </span>
            of
            <span class="font-semibold text-gray-900 dark:text-white">
              {{ total }}
            </span>
            Entries
        </span>
        <!-- Buttons -->
        <div class="inline-flex mt-2 xs:mt-0">
            <!-- Previous Button -->
            <button :class="{'pointer-events-none': current === 1}" @click="onPrevClick" class="py-2 px-4 text-sm font-medium text-white bg-gray-800 rounded-l hover:bg-gray-900 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
              <svg v-if="showIcons" class="mr-2 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M7.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l2.293 2.293a1 1 0 010 1.414z" clip-rule="evenodd"></path></svg>
                Prev
            </button>
            <!-- Next Button -->
            <button :class="{'pointer-events-none': current === totalPages}" @click="onNextClick" class="py-2 px-4 text-sm font-medium text-white bg-gray-800 rounded-r border-0 border-l border-gray-700 hover:bg-gray-900 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
                Next
                <svg v-if="showIcons" class="ml-2 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
            </button>
        </div>
      </div>
    </template>

    <!-- Navigation Layout -->
    <template v-else-if="layout === 'navigation'">
      <!-- Previous Button -->
      <a :class="{'pointer-events-none': current === 1}" @click="onPrevClick" href="#" class="inline-flex items-center py-2 px-4 text-sm font-medium text-gray-500 bg-white rounded-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
        <svg v-if="showIcons" class="mr-2 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M7.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l2.293 2.293a1 1 0 010 1.414z" clip-rule="evenodd"></path></svg>
        Previous
      </a>

      <!-- Next Button -->
      <a :class="{'pointer-events-none': current === totalPages}" @click="onNextClick" href="#" class="inline-flex items-center py-2 px-4 ml-3 text-sm font-medium text-gray-500 bg-white rounded-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
        Next
        <svg v-if="showIcons" class="ml-2 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
      </a>
    </template>

    <!-- Default Layout -->
    <template v-else>
      <ul class="inline-flex -space-x-px">
        <li>
          <!-- Previous Button -->
          <a :class="{'pointer-events-none': current === 1}" @click="onPrevClick" href="#" class="py-2 px-3 ml-0 leading-tight text-gray-500 bg-white rounded-l-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
            <svg v-if="showIcons" class="mr-2 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M7.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l2.293 2.293a1 1 0 010 1.414z" clip-rule="evenodd"></path></svg>
            Previous
          </a>
        </li>
        <li v-for="number in pageNumbers" :key="`pagination-num-${number}`">
          <a @click="onPageClick(number)" href="#" :class="{'pointer-events-none	': number === '...' || number === current, 'pointer-events-none text-blue-600 bg-blue-50 border border-gray-300 dark:border-gray-700 dark:bg-gray-700 dark:text-white': number === current, 'leading-tight text-gray-500 bg-white border border-gray-300 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400': number !== current}" class="py-2 px-3 hover:bg-gray-100 hover:text-gray-700 dark:hover:bg-gray-700 dark:hover:text-white">
            {{ number }}
          </a>
        </li>
        <li>
          <!-- Next Button -->
          <a :class="{'pointer-events-none': current === totalPages}" @click="onNextClick" href="#" class="py-2 px-3 leading-tight text-gray-500 bg-white rounded-r-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
            Next
            <svg v-if="showIcons" class="ml-2 w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
          </a>
        </li>
      </ul>
    </template>
  </nav>
</template>
<script lang="ts" setup>
import { computed, toRefs } from 'vue'
import type { PropType } from 'vue'
import type { Layout } from './types'

const props = defineProps({
  layout: {
    type: String as PropType<Layout>,
    default: 'pagination',
  },
  current: {
    type: Number,
    default: 1,
  },
  total: {
    type: Number,
    default: 50,
  },
  perPage: {
    type: Number,
    default: 10,
  },
  showIcons: {
    type: Boolean,
    default: false,
  },
  paginationItems: {
    type: Number,
    default: 7,
  },
})


const emit = defineEmits(['pageChange'])

const onNextClick = () => {
  emit('pageChange', props.current + 1)
}
const onPrevClick = () => {
  emit('pageChange', props.current - 1)
}
const onPageClick = (number) => {
  emit('pageChange', number)
}

const totalPages = computed(() => props.layout === 'table' ? Math.ceil(props.total / props.perPage) : props.total )

const paginationSize = computed(() => Math.floor(Math.max(props.paginationItems, 7) / 2) * 2 + 1 )

const pageNumbers = computed(() => {
  // console.log(paginationSize.value)
  if (totalPages.value <= paginationSize.value) {
    // All page numbers
    return Array.from({ length: totalPages.value }, (e, i) => i + 1)
  }
  const endLength = paginationSize.value - 2
  const pivotNumber = endLength - 1
  if (props.current <= pivotNumber) {
    // First pages
    return [
      ...Array.from({ length: endLength }, (e, i) => i + 1),
      '...',
      totalPages.value,
    ]
  }
  if (props.current > totalPages.value - pivotNumber) {
    // Last pages
    return [
      1,
      '...',
      ...Array.from({ length: endLength }, (e, i) => totalPages.value - pivotNumber + i),
    ]
  }
  // Middle pages
  const middleLength = Math.floor(paginationSize.value / 2) - 2
  return [
    1,
    '...',
    ...Array.from({ length: middleLength }, (e, i) => props.current - middleLength + i),
    props.current,
    ...Array.from({ length: middleLength }, (e, i) => props.current + i + 1),
    '...',
    totalPages.value,
  ]
})

</script>
