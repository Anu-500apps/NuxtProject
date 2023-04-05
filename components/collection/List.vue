<template>
     <collectionAdd @delete="emits('delete')"></collectionAdd>
    <collectionEdit @edit="emits('edit')"></collectionEdit>
</template>
<script setup lang="ts">
import {defineEmits} from 'vue'
const emits = defineEmits(['edit','delete'])
</script>