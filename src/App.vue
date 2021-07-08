<template>
    <MultiMenu/>
    <section class="w-full flex flex-col items-center">
        <image-slide />
        <task-list />
    </section>

</template>

<script>
    import MultiMenu from './components/MultiMenu.vue';
    import TaskList from './components/TaskList.vue';
    import ImageSlide from './components/Slide.vue';
    
    export default ({
        components: {
            MultiMenu,
            TaskList,
            ImageSlide
        },
    })
    
</script>
<style scoped>
    section {
        z-index: -2;
    }
    
    
</style>