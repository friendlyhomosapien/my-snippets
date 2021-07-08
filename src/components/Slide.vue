<template>
    <div class="container flex justify-between mt-20">
        <button class="text-4xl px-2 bg-red-500" @click="moveSlideLeft()">{{ `<` }}</button>
        <div class="slide_cover">
            <transition-group name="slide">
                <span
                    v-for="image in slide.images"
                    :key="image.pos"
                    class="image_container"
                >
                    <img src="avatars-ypCd5dE5YbGkyF0p-Y59d9w-t500x500.jpg"/>
                    {{ image.pos }}
                </span>
            </transition-group>
        </div>
        <button class="text-4xl px-2 bg-red-500" @click="moveSlideRight()">{{ `>` }}</button>
    </div>
</template>
<script>
export default {
    data() {
        return {
            slide: {
                images: [
                    {
                        src: '',
                        pos: 1
                    },
                    {
                        src: '',
                        pos: 2
                    },
                    {
                        src: '',
                        pos: 3
                    },
                    {
                        src: '',
                        pos: 4
                    },
                ]
            },
        }
    },
    methods: {
        moveSlideLeft() {
            let tmp = this.slide.images.shift();
            this.slide.images.push(tmp);
        },
        moveSlideRight() {
            let tmp = this.slide.images.pop();
            this.slide.images.unshift(tmp);
        },
    },
}
</script>
<style scoped>

.slide-move {
    transition: transform 400ms ease;
}
.slide_cover {
    display: flex;
    overflow-x: hidden;
}
.slide_cover .image_container {
    max-width: 200px;
    color: white;
}

</style>