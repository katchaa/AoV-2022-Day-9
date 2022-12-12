<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md flex flex-col items-center">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>
      <div class="mt-2 flex justify-center items-center">
        <img
          v-for="present in sortPresents"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <button
        @click="toggleSort()"
        class="bg-indigo-600 text-white px-3 py-2 mt-5 rounded-lg border border-black hover:bg-indigo-500 transition duration-200"
      >
        Toggle sort
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'
import presents from './presents.json'

const sortMethods = reactive({
  sorted: (x, y) => x.dimensions.width * x.dimensions.height - y.dimensions.width * y.dimensions.height,
  default: (x, y) => x.id - y.id,
})

let activeSortMethod = ref('default')

const toggleSort = () => {
  activeSortMethod.value = activeSortMethod.value === 'default' ? 'sorted' : 'default'
}

const sortPresents = computed(() => presents.sort(sortMethods[activeSortMethod.value]))
</script>
