<template>
    <div>
         <button
            type="button"
            class="rounded-md bg-gray-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
            @click="emits('edit')"
          >
            Edit
          </button>
           <button
            type="button"
            class="rounded-md bg-gray-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 ml-5"
            @click="Delete"
          >
            Delete
          </button>
    </div>
</template>
<script setup lang="ts">
import {defineEmits} from 'vue'
const emits = defineEmits(['edit','delete'])
</script>