<template>
    <MyMarkdownBlogs :path="props.path" git="/whispers-in-the-end--of-year/"/>

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