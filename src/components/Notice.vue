<script setup>

    import { ref, onMounted, onUnmounted } from 'vue'
    import { withBase } from '../utils/utils'
    
    import Title from './Title.vue'

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
    <div class="content_wrap notice_wrap z-20">
        <Title :infoData="infoData" />
        <div class="notice_box py-10 px-4 md:px-8 mx-auto max-w-[1240px]" data-aos="fade-up" data-aos-delay="500" data-aos-duration="1000">
            <div class="notice_info w-full bg-white py-12 px-6 sm:py-14 sm:px-10 md:py-16 md:px-12 mb-15">
                <ul class="notice_list list-disc pl-6 flex flex-col gap-4 text-left mx-auto max-w-[1080px]">
                    <li
                        v-for="(item, idx) in infoData.text"
                        :key="idx"
                        class="notice_text text-base sm:text-lg md:text-lg lg:text-lg font-semibold leading-relaxed tracking-wide"
                        v-html="item"
                    ></li>
                </ul>
            </div>
            <div class="notice_sign_up_box flex flex-col justify-between items-center gap-10 xl:flex-row">
                <div class="notice_sign_up_item w-fit">
                    <a :href="withBase('/SignUp')">
                        <img :src="withBase('go_to_sign_up_btn_1.svg')" class="go_to_sign_up_img h-15 sm:h-18" alt="sign up btn img">
                    </a>
                </div>
                <div class="notice_sign_up_item w-fit">
                    <a :href="withBase('/SignUpAlready')">
                        <img :src="withBase('go_to_sign_up_btn_2.svg')" class="go_to_sign_up_img h-15 sm:h-18" alt="sign up btn img">
                    </a>
                </div>
                <div class="notice_sign_up_item w-fit">
                     <a :href="withBase('/SignUpInstitution')">
                        <img :src="withBase('go_to_sign_up_btn_3.svg')" class="go_to_sign_up_img h-15 sm:h-18" alt="sign up btn img">
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .notice_wrap {
        padding-bottom: 180px !important;
    }

    @media screen and (max-width: 1024px) {
        .notice_wrap {
            padding-bottom: 140px !important;
        }
    }
    @media screen and (max-width: 768px) {
        .notice_wrap {
            padding-bottom: 120px !important;
        }
    }

    .notice_info {
        border-radius: 64px;
        box-shadow: 0px 4px 25px rgba(0, 0, 0, 0.08);
    }

    .notice_text {
        color: #65a3ff;

        // 不要段行:一律隱藏 pc_br 與 br
        :deep(.pc_br),
        :deep(br) {
            display: none;
        }
    }

    // 圓點顏色
    .notice_list li::marker {
        color: #65a3ff;
    }

    .go_to_sign_up_img{
        cursor: pointer;
        transition: .3s;
    }

    .go_to_sign_up_img:hover{
        transform: scale(1.1);
    }
    
    .sun_light{
        position: absolute;
        display: block;
        z-index: 2;
        left: 0.3%;
        right: 0;
        top: -100%;
        bottom: 0;
        margin: auto;
        width: 400rem;
        opacity: 1;
        mix-blend-mode: lighten;
        filter: blur(5px);
        transform: scale(1.6);
    }

    .waveWrapper {
        overflow: hidden;
        position: static;
        display: block;
        width: 100%;
        height: 100%;
        left: 0;
        right: 0;
        bottom: 0;
        top: 0;
        margin: auto;
        z-index: 2;
    }

    .kv_wave{
        position: absolute;
        display: block;
        width: 100%;
        bottom: 0;
    }

    @media screen and (max-width:1366px) {
        .sun_light{
            top: -100%;
            transform: scale(1.9);
        }
    }

    @media screen and (max-width:1024px) {
        .kv_wave{
            max-width: none;
            width: 400%;
            left: -150%;
        }

        .sun_light{
            top: -100%;
            transform: scale(3);
        }
    }

    @media screen and (max-width: 768px) {
        .sun_light{
            transform: scale(4);
        }
    }

</style>