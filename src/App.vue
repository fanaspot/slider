<template>
  <swiper
    :centeredSlides="true"
    :pagination="{
      clickable: true,
    }"
    :navigation="{
      prevEl: '.nav-btn-prev',
      nextEl: '.nav-btn-next',
    }"
    :modules="modules"
    @autoplayTimeLeft="onAutoplayTimeLeft"
    :breakpoints="{
      1024: {
        autoplay: {
          enabled: true,
          delay: 4000,
        },
      },
    }"
    class="mySwiper"
  >
    <swiper-slide v-for="(slide, index) in slides" :key="'slide' + index">
      <SlideComponent
        class="slide-container"
        :h1="slide.h1"
        :image="slide.image"
        :p="slide.p"
      />
    </swiper-slide>
    <template #container-end>
      <div class="nav-btns">
        <button class="nav-btn-prev">
          <img src="./assets/img/nav-icon.svg" />
        </button>
        <button class="nav-btn-next">
          <img
            src="./assets/img/nav-icon.svg"
            style="transform: rotate(180deg)"
          />
        </button>
        <div class="autoplay-progress">
          <svg viewBox="0 0 48 48" ref="progressCircle">
            <circle cx="24" cy="24" r="20"></circle>
          </svg>
          <span ref="progressContent"></span>
        </div>
      </div>
    </template>
  </swiper>
</template>
<script>
import { ref } from "vue";

import { Swiper, SwiperSlide } from "swiper/vue";

import "swiper/css";

import "swiper/css/pagination";
import "swiper/css/navigation";

import "./assets/css/main.css";

import { Autoplay, Pagination, Navigation } from "swiper/modules";

import SlideComponent from "./components/SlideComponent";

export default {
  components: {
    Swiper,
    SwiperSlide,
    SlideComponent,
  },
  setup() {
    const progressCircle = ref(null);
    const progressContent = ref(null);
    const onAutoplayTimeLeft = (s, time, progress) => {
      progressCircle.value.style.setProperty("--progress", 1 + progress);
    };
    const slides = ref([
      {
        h1: "Яркие дни — большие скидки на мебель",
        image: "slide1-min.png",
        p: "",
      },
      {
        h1: "Классические кухни",
        image: "slide2-min.png",
        p: "",
      },
      {
        h1: "Современные кухни",
        image: "slide3-min.png",
        p: "",
      },
    ]);
    return {
      onAutoplayTimeLeft,
      progressCircle,
      progressContent,
      slides,
      modules: [Autoplay, Pagination, Navigation],
    };
  },
};
</script>
