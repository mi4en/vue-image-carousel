<template>
    <div class="container">
        <div class="carousel-container">
            <i class="fas fa-chevron-left" id="prevBtn" @click="goPrevious()"></i>
            <i class="fas fa-chevron-right" id="nextBtn" @click="goNext()"></i>
            <div class="carousel-slide">
                <img v-for="image in images" :key="image.id" :src="image.download_url" alt="" />
            </div>
        </div>

        <div class="images-lineup">
            <img v-for="image in images" :key="image.id" :src="image.download_url" alt="" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'image-carousel',
    data() {
        return {
            images: [],
            counter: 0,
        };
    },
    methods: {
        async getImages() {
            try {
                const res = await axios.get('https://picsum.photos/v2/list?limit=5');
                console.log(res.data);
                this.images = res.data;
                return res;
            } catch (error) {
                console.log(error);
            }
        },
        goPrevious() {
            // The if else is used only to catch when we go from last to first so we speed the transition
        },
        goNext() {
            // The if else is used only to catch when we go from first to last so we speed the transition
        },
        focusPreviewedImg() {},
    },
    created() {
        this.getImages();
    },
};
</script>

<style scoped lang="scss">
.carousel-container {
    width: 60%;
    margin: 1rem auto;
    border: 1px solid #333;
    overflow: hidden;
    position: relative;

    .carousel-slide {
        display: flex;
        width: 100%;
        height: 500px;

        img {
            width: 100%;
            height: 500px;
        }
    }

    #prevBtn {
        position: absolute;
        top: 50%;
        z-index: 1;
        left: 5%;
        font-size: 50px;
        color: #fff;
        opacity: 0.8;
        cursor: pointer;
        transition: all 0.3s ease-in-out;
    }

    #prevBtn:hover {
        transform: scale(1.3);
    }

    #nextBtn {
        position: absolute;
        top: 50%;
        z-index: 1;
        right: 5%;
        font-size: 50px;
        color: #fff;
        opacity: 0.8;
        cursor: pointer;
        transition: all 0.3s ease-in-out;
    }

    #nextBtn:hover {
        transform: scale(1.3);
    }
}

.images-lineup {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 60%;
    margin: 1rem auto;

    img {
        width: 140px;
        height: 80px;
        margin-right: 5px;
        border: 1px solid purple;
        cursor: pointer;
        transition: all 0.2s ease-in-out;
        margin: 2px 2px;
    }
}

.previewed {
    border: 3px solid blue !important;
    transform: scale(1.3);
}
</style>
