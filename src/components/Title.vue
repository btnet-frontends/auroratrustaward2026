<script setup>
    import AOS from 'aos'
    import 'aos/dist/aos.css'
    import { onMounted } from 'vue'
    import titleActivity from '../assets/image/title_Activity.png'
    import titleAgenda from '../assets/image/title_Agenda.png'
    import titleInstitution from '../assets/image/title_Institution.png'
    import titleNotice from '../assets/image/title_Notice.png'

    const props = defineProps({
        infoData: Object
    });

    const titleImageMap = {
        '活動資訊': titleActivity,
        '活動議程': titleAgenda,
        '獲獎機構': titleInstitution,
        '報名資訊': titleNotice,
    };

    function getTitleImg(title) {
        const img = titleImageMap[title];
        if (!img) return null;
        return typeof img === 'object' && img.src ? img.src : img;
    }

    onMounted(() => {
        AOS.init()
    });
</script>

<template>
    <div :class="['title_area w-full text-center', infoData.title === '活動資訊' ? '' : 'pb-[35px]']" data-aos="fade-up" data-aos-delay="500" data-aos-duration="1000">
        <div v-if="getTitleImg(infoData.title)" :class="['title_box w-fit mx-auto', infoData.title === '活動資訊' ? 'event_info_title_box -mt-[12%] sm:-mt-[8%] md:-mt-[10%] pb-2' : 'py-5']">
            <img 
                :src="getTitleImg(infoData.title)" 
                :alt="infoData.title" 
                :class="[
                    'block mx-auto h-auto drop-shadow-sm',
                    infoData.title === '活動資訊' 
                        ? 'w-[240px] sm:w-[280px] md:w-[300px]' 
                        : 'w-[270px] sm:w-[320px] md:w-[360px]'
                ]"
            />
        </div>
        <div v-else class="title_box w-fit py-5 mx-auto">
            <h1 :style="{ color: infoData.titleColor}" class="title text-5xl sm:text-6xl">{{ infoData.title }}</h1>
            <p :style="{ color: infoData.titleEnColor}" class="titleEn mt-1 text-sm sm:text-lg">{{ infoData.titleEn }}</p>
        </div>
    </div>
</template>

<style scoped>
    .title_box h1{
        font-family: "Noto Serif TC", serif;
        font-optical-sizing: auto;
        font-weight: 600;
        font-style: normal;
        letter-spacing: 0.3rem;
    }
    .title_box p{
        font-family: "Noto Serif TC", serif;
        font-optical-sizing: auto;
        font-weight: 600;
        font-style: normal;
    }

    .event_info_title_box{
        position: relative;
        display: block;
        border-radius: 20px;
    }

    .event_info_title{
        font-family: "Chiron GoRound TC", sans-serif !important;
        font-optical-sizing: auto !important;
        font-weight: 400 !important;
        font-style: normal !important;
    }

    .event_info_title_bg{
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        margin: 0 auto;
        width: 14rem;
        height: 4.5rem;
        z-index: -1;
        border-radius: 20px;
    }
</style>