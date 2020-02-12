<template>
    <div class="container">
        <div class="carousel-container">
            <i class="fas fa-chevron-left" id="prevBtn" @click="goPrevious()"></i>
            <i class="fas fa-chevron-right" id="nextBtn" @click="goNext()"></i>
            <transition-group name="slide-fade" tag="div" class="carousel-slide">
                <!-- <img :src="activeImage.download_url" alt="no_image" /> -->
                <div v-for="i in [counter]" :key="i">
                    <img :src="activeImage.download_url" />
                </div>
            </transition-group>
        </div>

        <div class="images-lineup">
            <img
                v-for="(image, index) in images"
                :key="image.id"
                :src="image.download_url"
                :class="image.id === activeImage.id ? 'previewed' : ''"
                @click="selectFromLineup(index)"
                alt="some_img"
            />
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
            activeImage: {},
        };
    },
    methods: {
        async getImages() {
            try {
                const res = await axios.get('https://picsum.photos/v2/list?limit=5');
                console.log(res.data);
                this.images = res.data;
                this.activeImage = this.images[0];
                console.log('active: ', this.activeImage);
                return res;
            } catch (error) {
                console.log(error);
            }
        },
        goNext() {
            if (this.counter >= this.images.length - 1) {
                this.counter = 0;
                this.activeImage = this.images[this.counter];
            } else {
                this.counter++;
                this.activeImage = this.images[this.counter];
            }
        },
        goPrevious() {
            if (this.counter <= 0) {
                this.counter = this.images.length - 1;
                this.activeImage = this.images[this.counter];
            } else {
                this.counter--;
                this.activeImage = this.images[this.counter];
            }
        },
        selectFromLineup(imageIndex) {
            this.counter = imageIndex;
            this.activeImage = this.images[this.counter];
        },
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

        .slide-fade-enter-active {
            transition: all 0.5s ease-in;
        }
        .slide-fade-enter,
        .slide-fade-leave-to {
            transform: translateX(10px);
            opacity: 0.7;
        }

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
    border: 3px solid yellow !important;
    transform: scale(1.3);
}
</style>
