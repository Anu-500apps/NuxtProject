<template>
     <collectionAdd ></collectionAdd>
    <collectionEdit @edit="emits('edit')" @delete="emits('delete')"></collectionEdit>
</template>
<script setup lang="ts">
import {defineEmits} from 'vue'
const emits = defineEmits(['edit','delete'])
</script>