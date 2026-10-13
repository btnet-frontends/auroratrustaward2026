<script setup>
    import AOS from 'aos'
    import 'aos/dist/aos.css'

    import { getWindowWidth, getDivResize, withBase } from '../utils/utils'
    import { ref, onMounted, onUnmounted } from 'vue'

    const windowWidth = ref(0);
    const setDivResize = ref({});

    function handleResize() {
        windowWidth.value = getWindowWidth();
        setDivResize.value = getDivResize('.kv_area');

        // console.log('setDivResize:', setDivResize.value.width);
        // console.log('setDivResize:', setDivResize.value.height);
    }

    onMounted(() => {
        AOS.init()
        handleResize();
        window.addEventListener('resize', handleResize);

        const canvas = document.getElementById('aestheticCanvas');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let stars = [];
        const starCount = 120;

        for (let i = 0; i < starCount; i++) {
            stars.push({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            radius: Math.random() * 1.5 + 0.5,
            alpha: Math.random(),
            delta: (Math.random() * 0.02 + 0.005) * (Math.random() < 0.5 ? -1 : 1)
            });
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            for (let star of stars) {
            ctx.beginPath();
            ctx.arc(star.x, star.y, star.radius, 0, Math.PI * 2);
            ctx.fillStyle = `rgba(255, 255, 255, ${star.alpha})`;
            ctx.shadowBlur = 10;
            ctx.shadowColor = '#bb86fc';
            ctx.fill();

            star.alpha += star.delta;
            if (star.alpha <= 0 || star.alpha >= 1) star.delta *= -1;
            }

            requestAnimationFrame(draw);
        }

        draw();

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    });

    onUnmounted(() => {
        window.removeEventListener('resize', handleResize);
    });

</script>

<template>
    <div :class="['kv_area', { 'pc': windowWidth >= 1024 }, { 'mb': windowWidth < 1024}]">
        <div class="kv_box" :style="{ width: setDivResize.width + 'px', height: setDivResize.height + 'px' }">
            <img :src="withBase('kv_big_title.svg')" class="kv_img" alt="kv_img">
        </div>

        <span class="sparkle sparkle-1" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-2" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-3" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-4" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-5" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-6" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-7" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
        <span class="sparkle sparkle-8" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
<span class="sparkle sparkle-9" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>
<span class="sparkle sparkle-10" aria-hidden="true"><span class="spark-line"></span><span class="spark-core"></span></span>

    </div>
</template>

<style scoped>
    .kv_area{
        position: relative;
        display: block;
        width: 100%;
        height: 100vh;
        background: url('../assets/image/kv_bg.png') center center no-repeat;
        background-size: cover;
        overflow: hidden;
        text-align: center;
    }

    .kv_area.pc{
        min-height: 580px;
    }

    .kv_box{
        position: absolute;
        display: block;
        left: 0;
        right: 0;
        top: 5%;
        bottom: 0;
        margin: auto;
        z-index: 3;
    }

    .kv_img{
        position: absolute;
        display: block;
        z-index: 3;
        left: 0;
        right: 0;
        top: -45%;
        bottom: 0;
        margin: auto;
        width: 55%;
    }
    .sun_light{
        position: absolute;
        display: block;
        z-index: 2;
        left: 0.3%;
        right: 0;
        top: -24%;
        bottom: 0;
        margin: auto;
        width: 400rem;
        opacity: 1;
        mix-blend-mode: lighten;
        filter: blur(5px);
        transform: scale(1.2);
    }

    .sparkle{
        position: absolute;
        z-index: 5;
        width: 100px;
        height: 14px;
        pointer-events: none;
        opacity: 0;
        animation: sparkle-twinkle 2.4s ease-in-out infinite;
        animation-delay: var(--delay, 0s);
        will-change: opacity;
    }
    .sparkle .spark-line{
        position: absolute;
        top: 50%;
        left: 0;
        width: 100%;
        height: 1.5px;
        background: linear-gradient(90deg, transparent 0%, rgba(255,255,255,0.9) 50%, transparent 100%);
        transform: translateY(-50%);
        mix-blend-mode: screen;
        filter: drop-shadow(0 0 3px rgba(255,255,255,0.7));
    }
    .sparkle .spark-core{
        position: absolute;
        top: 50%;
        left: 50%;
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background: radial-gradient(circle, rgba(255,255,255,1) 0%, rgba(255,255,255,0.6) 55%, rgba(255,255,255,0) 100%);
        transform: translate(-50%, -50%) scale(0.4);
        mix-blend-mode: screen;
        box-shadow: 0 0 6px 1px rgba(255,255,255,0.7);
        animation: sparkle-core-pulse 2.4s ease-in-out infinite;
        animation-delay: var(--delay, 0s);
    }

    @keyframes sparkle-twinkle{
        0%, 100% { opacity: 0; }
        50%      { opacity: 1; }
    }
    @keyframes sparkle-core-pulse{
        0%, 100% { transform: translate(-50%, -50%) scale(0.4); }
        50%      { transform: translate(-50%, -50%) scale(1.1); }
    }

      .sparkle-1{ --delay: 0s;    top: 20%; left: 93%; transform: translate(-50%, -50%) rotate(-45deg) scale(1); }
    .sparkle-2{ --delay: 0.5s;  top: 28%; left: 90%; transform: translate(-50%, -50%) rotate(-35deg) scale(2); }
    .sparkle-3{ --delay: 1s;    top: 83%; left: 50%; transform: translate(-50%, -50%) rotate(-25deg) scale(1.1); }
    .sparkle-4{ --delay: 1.5s;  top: 73%; left: 23%; transform: translate(-50%, -50%) rotate(-2deg)  scale(2); }
    .sparkle-5{ --delay: 2s;    top: 87%; left: 35%; transform: translate(-50%, -50%) rotate(-4deg)  scale(3); }
    .sparkle-6{ --delay: 2.5s;  top: 24%; left: 79%; transform: translate(-50%, -50%) rotate(-40deg) scale(1); }
    .sparkle-7{ --delay: 3s;    top: 64%; left: 20%; transform: translate(-50%, -50%) rotate(20deg)  scale(1); }
    .sparkle-8{ --delay: 4s;  top: 68%; left: 10%; transform: translate(-50%, -50%) rotate(20deg)  scale(1); }
    .sparkle-9{ --delay: 4s;    top: 48%; left: 90%; transform: translate(-50%, -50%) rotate(-25deg) scale(2); }
.sparkle-10{ --delay: 4.5s; top: 67%; left: 55%; transform: translate(-50%, -50%) rotate(-16deg)   scale(2); }
    @media (prefers-reduced-motion: reduce){
        .sparkle{ animation-duration: 4.8s; }
        .sparkle .spark-core{ animation-duration: 4.8s; }
    }

    @media screen and (max-width: 1024px){
        .sparkle{ display: none; }
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
    canvas {
        position: absolute;
        display: block;
        z-index: 6;
        height: 50%;
        bottom: 0;
    }
    .kv_wave{
        position: absolute;
        display: block;
        width: 100%;
        bottom: 0;
    }
    @keyframes bob-1   { from { bottom: -23px   } to { bottom: 0 } }
    @keyframes bob-2   { from { bottom: -30px   } to { bottom: 0} }
    @keyframes bob-3   { from { bottom: -30px   } to { bottom: 0  } }
    @keyframes bob-4   { from { bottom: -25px   } to { bottom: 0 } }

    .kv_wave_light{
        z-index: 5;
        mix-blend-mode: screen;
        opacity: 0.5;
        will-change: bottom;
    }
    

    @media (prefers-reduced-motion: reduce) {
        .kv_wave, .kv_wave_light { animation: none !important; }
    }





    @media screen and (max-width:1920px) {
        .kv_img{
            width: 60%;
        }
        .sun_light{
            transform: scale(1.8);
            top: -24%;
        }
    }

    
    @media screen and (max-width:1366px) {
        .kv_box {
            top: -15%;
        }
         .kv_img{
            width: 70%;
        }
        .sun_light{
            top: -44%;
            transform: scale(1.9);
        }
    }

    @media screen and (max-width:1280px) {
        /* .kv_box {
            top: -5%;
        } */
    }

    @media screen and (max-width:1024px) {
        .kv_area{
            height: 100vh;
            background: url('../assets/image/kv_bg.png') center center no-repeat;
            background-size: cover;
        }

        .kv_area.mb{
            min-height: 1355px;
        }

        .kv_box {
            top: -9%;
        }

        .kv_img{
            width: 78%;
            top:-50px;
        }
        .sun_light{
            top: -41%;
            transform: scale(3);
        }

        .kv_wave{
            max-width: none;
            width: 400%;
            left: -150%;
        }
    }


    @media screen and (max-width:820px) {
        .kv_area.mb{
            min-height: 1125px;
        }
    }

    @media screen and (max-width: 768px) {
        .kv_area.mb{
            min-height: 667px;
        }
        .kv_img{
            width: 100%;
        }
        .sun_light{
            transform: scale(4);
        }

    }

    @media screen and (max-width: 560px) {
        .kv_smart_logo{
            top: -27%;
            left: 0%;
            right: 0%;
            width: 50%;
            margin: 0 auto;
        }

        .sun_light{
            top: -32%;
        }
    }
</style>