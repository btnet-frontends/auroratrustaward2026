<script setup>

    import { ref, onMounted, onUnmounted } from 'vue'
    
    import Title from './Title.vue'

    import { getWindowWidth, withBase} from '../utils/utils'

    import AOS from 'aos'
    import 'aos/dist/aos.css'
    

    defineProps(
        {
            infoData: Object
        }
    );

    const width = ref(0);

    function handleResize() {
        width.value = getWindowWidth()
    }

    onMounted(() => {
        AOS.init()
        window.addEventListener('resize', handleResize)
    });

    onUnmounted(() => {
        window.removeEventListener('resize', handleResize)
    });


</script>

<template>
    <div class="content_wrap activity_content_wrap z-10">
        <div class="activity_box relative flex flex-col justify-start w-full py-10 px-10 md:px-20 xl:mx-auto xl:flex-row" data-aos="fade-up" data-aos-delay="500" data-aos-duration="1000">
            <div class="activity_item relative flex flex-col justify-center items-center xl:items-start px-0 w-full mx-auto mb-6 xl:mx-0 xl:w-auto xl:px-10 xl:min-w-[420px]">
                <Title :infoData="infoData" />
                <picture>
                    <source media="(max-width: 768px)" :srcset="withBase('ball_bg_mb.png')" />
                    <img class="ball_bg_img" :src="withBase('ball_bg.png')" alt="ball bg" />
                </picture>
                <div class="date_box z-10 flex flex-row items-end mb-2">
                    <h1 class="date z-10 text-[5rem] md:text-[7rem] font-bold leading-none" style="color:#fff;">{{infoData.date1}}</h1>
                    <span class="week z-10 mb-4 ml-1 text-[1.6rem] md:text-[2rem]" style="color:#fff;">{{infoData.date2}}</span>
                </div>
                <div class="time_bar z-10 flex flex-row items-center px-3 py-1 mb-4">
                    <span class="time_gradient_text">
                        <span class="text-[1.2rem] md:text-[1.5rem] font-semibold">{{infoData.time}}</span>
                        <span class="text-[1rem] md:text-[1.2rem] ml-1">{{infoData.opneTime}}</span>
                    </span>
                </div>
                <div class="location_box z-10 flex flex-col justify-start items-center xl:items-start">
                    <h1 class="location mb-1 text-xl md:text-2xl font-bold text-center xl:text-left" style="color:#fff;">{{infoData.location}}</h1>
                    <p class="location_info text-base md:text-xl text-center xl:text-left" style="color:#fff;">{{infoData.locationInfo}}</p>
                </div>
            </div>
            <div class="activity_item relative z-10 flex flex-col justify-center items-center mx-auto w-full xl:flex-1 xl:mx-0">
                <iframe class="google_map_iframe overflow-hidden rounded-xl" :src="infoData.googleMap" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .time_gradient_text{
        background: #fe508b;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        color: transparent;
    }
    .time_bar{
        background: rgba(255, 255, 255, 0.9);
        backdrop-filter: blur(4px);
        border-radius: 0;
    }
    .activity_content_wrap {
        padding-bottom: 220px !important;
    }

    .ball_bg_img{
        position: absolute;
        display: block;
        z-index: -1;
        top: 65%;
        left: -15rem;
        transform: translateY(-50%);
        width: 210%;
        max-width: 1280px;
        pointer-events: none;
        opacity: 0.9;
    }
    .google_map_iframe{
        box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.3);
        width: 690px;
        height: 475px;
        max-width: 100%;
    }

    @media screen and (max-width: 1280px) {
        .activity_content_wrap {
            padding-bottom: 180px !important;
        }
        .ball_bg_img{
            width: 185%;
            left: -7rem;
            top: 52%;
        }
    }
    @media screen and (max-width: 1024px) {
        .activity_content_wrap {
            padding-bottom: 150px !important;
        }
        .ball_bg_img{
            width: 165%;
            left: -8rem;
            top: 62%;
        }
        .google_map_iframe{
            width: 100%;
            height: 380px;
        }
    }
    @media screen and (max-width: 768px) {
        .activity_content_wrap {
            padding-bottom: 130px !important;
        }
        .ball_bg_img{
            width: 180%;
            left: -5.5rem;
            top: 65%;
        }
        .google_map_iframe{
            width: 100%;
            height: 300px;
        }
    }
</style>