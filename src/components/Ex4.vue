<script setup>
    import ViewPosts from './ViewPosts.vue';
    import { ref } from 'vue';

    const isEdit = ref(false);

    
</script>

<template>
    <ViewPosts />
    <div v-if="isEdit">
        <h2>Edit Post</h2>
    </div>
</template>