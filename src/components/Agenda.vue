<script setup>
    import Title from './Title.vue'
    import { onMounted } from 'vue'

    import AOS from 'aos'
    import 'aos/dist/aos.css'

    defineProps({
        infoData: Object
    });

    const tagKeywords = ['專題演講', '表演團體', '頒獎典禮'];

    function parseTopic(topic) {
        if (!topic) return { isTag: false, tag: '', subTopic: '', rawTopic: '' };
        
        if (topic.includes('<br>')) {
            const parts = topic.split('<br>');
            return {
                isTag: true,
                tag: parts[0].trim(),
                subTopic: parts[1] ? parts[1].trim() : '',
                rawTopic: topic
            };
        }
        
        const isMatchedTag = tagKeywords.some(keyword => topic.includes(keyword));
        if (isMatchedTag) {
            return {
                isTag: true,
                tag: topic.trim(),
                subTopic: '',
                rawTopic: topic
            };
        }

        return {
            isTag: false,
            tag: '',
            subTopic: '',
            rawTopic: topic
        };
    }

    onMounted(() => {
        AOS.init()
    });

</script>

<template>
    <div class="content_wrap agenda_wrap relative z-10">
        <Title :infoData="infoData" />
        <div class="agenda_box max-w-[1200px] px-4 md:px-6 lg:px-8 pb-8 xl:mx-auto" data-aos="fade-up" data-aos-delay="500" data-aos-duration="1000">
            <div class="agenda_table flex flex-col gap-4 md:gap-5 pb-4">
                <div 
                    v-for="(item, idx1) in infoData.agendaInfo" 
                    :key="idx1" 
                    :class="['agenda_table_item flex flex-col md:flex-row px-5 md:px-6 lg:px-10 items-start md:items-center justify-between gap-2 md:gap-4 lg:gap-6', idx1 % 2 === 0 ? 'bg-light-blue' : 'bg-white']"
                >
                    <div class="time_box w-full md:w-[18%] lg:w-[20%] shrink-0 flex items-center justify-start md:justify-center">
                        <p class="w-full text-left md:text-center text-sm sm:text-base md:text-base lg:text-lg xl:text-xl font-semibold tracking-wide agenda_blue_text">{{ item.time }}</p>
                    </div>

                    <div class="agenda_topic_box w-full md:w-[46%] lg:w-[43%] flex flex-col justify-center items-start gap-1">
                        <template v-if="parseTopic(item.topic).isTag">
                            <span class="pink_tag inline-block text-white text-xs sm:text-sm md:text-xs lg:text-sm font-bold px-2.5 sm:px-3.5 py-0.5 rounded-lg">
                                {{ parseTopic(item.topic).tag }}
                            </span>
                            <span v-if="parseTopic(item.topic).subTopic" class="text-sm sm:text-base md:text-[15px] lg:text-base xl:text-lg font-semibold tracking-wide agenda_blue_text leading-tight">
                                {{ parseTopic(item.topic).subTopic }}
                            </span>
                        </template>
                        <template v-else>
                            <p class="text-sm sm:text-base md:text-base lg:text-lg xl:text-xl font-semibold tracking-wide agenda_blue_text" v-html="item.topic"></p>
                        </template>
                    </div>

                    <div class="speaker_area w-full md:w-[36%] lg:w-[37%] flex flex-col justify-center gap-1 md:items-start">
                        <div v-for="(sp, idx2) in item.speaker" :key="idx2" class="speaker_box flex flex-wrap items-baseline gap-x-2 text-sm sm:text-base md:text-[15px] lg:text-base xl:text-lg font-semibold agenda_blue_text leading-snug">
                            <span v-if="sp.speakerTitle" v-html="sp.speakerTitle"></span>
                            <span v-if="sp.speakerName" class="font-bold">{{ sp.speakerName }}</span>
                            <span v-if="sp.speakerNameEN" class="text-xs text-neutral-400 font-normal block w-full" v-html="sp.speakerNameEN"></span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .agenda_wrap {
        padding-bottom: 160px !important;
    }

    .agenda_box{
        position: relative;
        display: block;
        z-index: 10 !important;
    }

    .agenda_table_item{
        box-shadow: 0px 7px 15px rgba(0, 0, 0, 0.25);
        border-radius: 0;
        height: 6.25rem;
    }

    .bg-light-blue {
        background-color: #f3fcff;
    }

    .bg-white {
        background-color: #ffffff;
    }

    .agenda_blue_text {
        color: #65a3ff;
        font-weight: 600;
    }

    .pink_tag {
        background-color: #fe508b;
        color: #ffffff;
        font-weight: 700;
        border-radius: 8px;
    }

    @media screen and (max-width: 1024px) {
        .agenda_wrap {
            padding-bottom: 120px !important;
        }
    }
    @media screen and (max-width: 768px) {
        .agenda_wrap {
            padding-bottom: 100px !important;
        }
        .agenda_table_item {
            height: auto;
            min-height: 5.5rem;
            padding: 1.25rem 1.25rem;
        }
    }
</style>
