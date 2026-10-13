<script setup>

    import { ref, onMounted, onUnmounted } from 'vue'
    
    import Title from './Title.vue'
    import { withBase } from '../utils/utils'

    import AOS from 'aos'
    import 'aos/dist/aos.css'
    

    defineProps(
        {
            infoData: Object
        }
    );

    onMounted(() => {
        AOS.init()
    });


</script>

<template>
    <div class="content_wrap intro_wrap relative">
        <picture>
            <source media="(max-width: 768px)" :srcset="withBase('ball_bg_mb.png')" />
            <img class="intro_ball_bg" :src="withBase('ball_bg.png')" alt="ball bg" />
        </picture>
        
        <Title :infoData="infoData" class="relative z-10" />
        
        <div class="intro_box relative z-10 max-w-[1200px] pt-1 pb-4 px-10 md:px-20 mx-5 xl:mx-auto" data-aos="fade-up" data-aos-delay="500" data-aos-duration="1000">
            <div class="intro_text intro_text1" v-for="(item, idx) in infoData.text" :key="idx">
                <p v-html="item"></p>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .intro_wrap {
        position: relative;
        padding-top: 150px !important;
        padding-bottom: 280px !important;
    }

    .intro_ball_bg {
        position: absolute;
        display: block;
        z-index: 0;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 120%;
        max-width: 1200px;
        pointer-events: none;
        opacity: 0.9;
    }

    :deep(.title_area) {
        padding-bottom: 0 !important;
    }
    :deep(.title_box) {
        margin-bottom: 1.5rem !important;
        padding-bottom: 0.25rem !important;
    }

    .intro_text{
        font-size: 1.8rem;
        margin-bottom: 1.5rem;
        letter-spacing: 3px;
        text-align: center;
    }
    .intro_text:last-child{
        margin-bottom: 0;
    }
    .intro_text p{
        color: #ffffff;
        font-family: "Chiron GoRound TC", sans-serif;
        font-optical-sizing: auto;
        font-weight: 300;
        font-style: normal;
        text-shadow: 0 1px 6px rgba(0, 0, 0, 0.15);
    }

    @media screen and (max-width: 1200px) {
        .intro_ball_bg {
            width: 130%;
            max-width: 1200px;
        }
    }
    @media screen and (max-width: 1024px) {
        .intro_wrap {
            padding-top: 130px !important;
            padding-bottom: 220px !important;
        }
        .intro_text{
            font-size: 1.6rem;
            letter-spacing: 3px;
        }
        .intro_ball_bg {
            width: 125%;
            max-width: 1050px;
        }
    }
    @media screen and (max-width: 768px) {
        .intro_wrap {
            padding-top: 100px !important;
            padding-bottom: 170px !important;
        }
        .intro_text{
            font-size: 1.3rem;
            letter-spacing: 2px;
        }
        .intro_text p{
            font-weight: 300;
        }
        .intro_ball_bg {
            width: 135%;
            max-width: 680px;
            top: 50%;
        }
    }
    @media screen and (max-width: 560px) {
        .intro_text{
            text-align: justify;
        }
        .intro_ball_bg {
            width: 200%;
            max-width: 1000px;
            top: 50%;
        }
    }
</style>