<template>
    <MyMarkdownBlogs :path="props.path" git="/year-end-fragmented-thoughts/"/>

</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import MyMarkdownBlogs from '@/components/MyMarkdownBlogs.vue';
const props = defineProps({
    path: {
        type: Array as () => Array<string>,
        default: () => [],
    },});
</script>