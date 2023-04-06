<template>
    <div>
        <div
          v-for="(templates,index) in templateData"
          :key="index"
          class="border p-4 rounded-md mb-3 shadow-sm bg-white"
        >
          <section>
            <h5 class="font-[500] text-md mb-2">{{ templates.name }}</h5>
            <span class="font-[500] text-md mb-2">{{ templates.subject }}</span>
            <span class="font-[500] text-md mb-2 ml-4">{{
              templates.body
            }}</span>
          </section>
          <collectionEdit @delete-templates="emits('delete-templates',templates)" @edit-templates="emits('edit-templates',templates,index)"></collectionEdit>
        </div>
      </div>
</template>
<script setup lang="ts">
import {defineEmits} from 'vue'
// Declare Emits Here
const emits = defineEmits(['edit-templates','delete-templates'])
const props = defineProps({
  // Declare props
  templateData: Array,
});
</script>