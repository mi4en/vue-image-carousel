<template>
    <div id="app">
        <image-carousel v-if="images.length > 0" :images="images" />
    </div>
</template>

<script>
import axios from 'axios';
import ImageCarousel from './components/ImageCarousel';

export default {
    name: 'App',
    components: {
        ImageCarousel,
    },
    data() {
        return {
            images: [],
        };
    },
    methods: {
        // Get images for the image-carousel component
        async getImages() {
            try {
                const res = await axios.get('https://picsum.photos/v2/list?limit=5');
                this.images = res.data;
                return res;
            } catch (error) {
                console.log(error);
            }
        },
    },
    async created() {
        this.getImages();
    },
};
</script>

<style lang="scss">
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
</style>
