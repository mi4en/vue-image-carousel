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
    // methods: {
    //     async getImages() {
    //         try {
    //             const res = await axios.get('https://picsum.photos/v2/list?limit=5');
    //             console.log(res.data);
    //             this.images = res.data;
    //             this.activeImage = this.images[0];
    //             console.log('active: ', this.activeImage);
    //             return res;
    //         } catch (error) {
    //             console.log(error);
    //         }
    //     },
    // },
    async created() {
        try {
            const res = await axios.get('https://picsum.photos/v2/list?limit=5');
            console.log(res.data);
            this.images = res.data;
        } catch (error) {
            console.log(error);
        }
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
