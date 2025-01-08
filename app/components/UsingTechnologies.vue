<template>
    <v-container class="cont-swiper">
        <!-- Стрелка назад, отображается только если не на первом слайде -->
        <v-icon class="arrow" :class="{ 'hidden': currentIndex === 0 }" @click="goToPrevSlide">
            mdi mdi-arrow-left
        </v-icon>

        <swiper :grabCursor="true" :effect="'creative'" :creativeEffect="{
            prev: {
                shadow: true,
                translate: [0, -70, -200],
                zIndex: -1,
            },
            next: {
                translate: ['100%', 0, 0],
            },
        }" :modules="modules" class="mySwiper" @slideChange="onSlideChange">
            <swiper-slide>
                <v-card class="card" elevation="0">
                    <v-card-title class="cardtitle">
                        👋 I'm Alex!
                    </v-card-title>
                    <v-card-text class="cardtext">
                        I create websites using vue, nuxt, react, vuetify and use tools such as axios, swiper.js, REST
                        API,
                        vuex, I've been studying frontend since 2022. I also do adaptive and cross-browser layout.
                    </v-card-text>
                    <v-row>
                        <a href="https://axios-http.com/docs/intro">
                            <v-btn class="logocard">
                                <img src="../assets/axios.png" alt="" class="logo">
                            </v-btn>
                        </a>
                        <a href="https://vuetifyjs.com/en/">
                            <v-btn class="logocard">
                                <img src="../assets/logo.svg" alt="" class="logo">
                            </v-btn>
                        </a>
                        <a href="https://vuejs.org/guide/introduction.html">
                            <v-btn class="logocard">
                                <img src="../assets/vue-logo.svg" alt="" class="logo">
                            </v-btn>
                        </a>
                        <a href="https://swiperjs.com/swiper-api"><v-btn class="logocard">
                                <img src="../assets/swiper.png" alt="" class="logo">
                            </v-btn></a>
                        <a href="https://swiperjs.com/swiper-api">
                            <v-btn class="logocard">
                                <img src="../assets/nuxt.svg" alt="" class="logo">
                            </v-btn>
                        </a>
                    </v-row>
                </v-card>
            </swiper-slide>
            <swiper-slide>
                <v-card class="card" elevation="0">
                    <v-card-text class="cardtext">

                    </v-card-text>
                </v-card>
            </swiper-slide>
            <swiper-slide>
                <v-card class="card" elevation="0">
                    <v-card-text class="cardtext">

                    </v-card-text>
                </v-card>
            </swiper-slide>
        </swiper>

        <!-- Скрытый контейнер для скрытых элементов (можно использовать для других целей) -->
        <v-container class="hidden-nextslide"></v-container>

        <!-- Стрелка вперед, отображается только если не на последнем слайде -->
        <v-icon class="arrow" :class="{ 'hidden': currentIndex === totalSlides - 1 }" @click="goToNextSlide">
            mdi mdi-arrow-right
        </v-icon>
    </v-container>
</template>

<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/effect-creative';
import { EffectCreative } from 'swiper/modules';
import { ref } from 'vue';

const modules = [EffectCreative];

// Используем реактивные переменные
const currentIndex = ref(0);
const totalSlides = ref(0);

// Функция для отслеживания изменения слайда
function onSlideChange(swiper) {
    currentIndex.value = swiper.realIndex;
    totalSlides.value = swiper.slides.length;
    console.log(currentIndex.value, totalSlides.value); // Лог для отладки
}

// Переход на предыдущий слайд
function goToPrevSlide() {
    const swiperInstance = document.querySelector('.mySwiper').swiper;
    swiperInstance.slidePrev();
}

// Переход на следующий слайд
function goToNextSlide() {
    const swiperInstance = document.querySelector('.mySwiper').swiper;
    swiperInstance.slideNext();
}
</script>




<style scoped>
#app {
    height: 100%
}

html,
body {
    position: relative;
    height: 100%;
}

body {
    background: #eee;
    font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
    font-size: 14px;
    color: #000;
    margin: 0;
    padding: 0;
}

.arrow {
    transition: opacity 0.3s ease, transform 0.3s ease;
    /* Плавное изменение прозрачности и движения */
}

.arrow.hidden {
    opacity: 0;
    /* Скрыть стрелку */
    transform: translateX(20px);
    /* Смещаем стрелку, чтобы она не была видна */
}

.logo {
    width: 30px;
}

.arrow:not(.hidden) {
    opacity: 1;
    /* Видимая стрелка */
    transform: translateX(0);
    /* Возвращаем стрелку в исходное положение */
}

.swiper {
    width: 90%;
    height: 70%;
    max-width: 1030px;
    max-height: 300px;
    overflow: visible;
}

.arrow {
    z-index: 3;
    scale: 1.2;
}

.cont-swiper {
    min-width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
}

.v-row {
    gap: 10px;
    padding: 30px;
}

.swiper-slide {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    font-weight: bold;
    color: #fff;
    border-radius: 15px;
    background-color: rgb(var(--v-theme-background));
}

.hidden-nextslide {
    width: 36px;
    height: 100%;
    position: absolute;
    top: 0;
    right: 0;
    display: flex;
    z-index: 2;

    background-color: rgb(var(--v-theme-background));
}

.card {
    min-width: 100%;
    min-height: 100%;
    border-radius: 15px;
}

.logocard {
    padding: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.cardtitle {
    margin-top: 20px;
    font-size: 30px;
}

.cardtext {
    font-size: 20px;
    margin-top: 10px;
}

@media (max-width: 1130px) {
    .cont-swiper {
        min-height: 400px;
        height: auto;
        max-width: 730px !important;
        min-width: auto;
        overflow: hidden;
    }

    .hidden-nextslide {
        width: 90%;
        translate: 0px 20px;
    }

    .swiper {
        max-height: 100%;
    }
}

@media (min-width: 501px) {
    .cont-swiper {
        min-height: 400px;
        height: auto;
        max-width: 730px !important;
        min-width: auto;
        overflow: hidden;
    }

    .swiper {
        max-height: 100%;
        height: auto;
        min-height: 467.5px;
    }

    .hidden-nextslide {
        width: 90%;
        right: -605px;
        translate: 0px 20px;
    }

    .card {
        max-height: 100%;
        height: auto;
        min-height: 467.5px;
    }

}

@media (max-width: 730px) {
    .hidden-nextslide {
        width: calc(8% + 13px);
        right: -10px;
        margin: 0;
        padding: 0;
    }

    .swiper {
        max-height: 80%;

        right: 0;
        height: auto;
        left: 0;
    }
}

@media (max-width: 500px) {
    .cont-swiper {
        min-height: 100%;
        min-width: 100%;
    }

    .swiper {
        max-height: 100%;
        height: auto;
        min-height: 467.5px;
    }

    .card {
        max-height: 100%;
        height: auto;
        min-height: 467.5px;
    }

}
</style>
