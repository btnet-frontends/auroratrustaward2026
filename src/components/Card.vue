<script setup>
    import { withBase } from '../utils/utils'
    
    const props = defineProps({
        institutionData: Object
    });

    const emit = defineEmits(['show-popup']);

    function openPopup(e) {
        if (e) {
            e.stopPropagation();
        }
        emit('show-popup', props.institutionData);
    }
</script>

<template>
    <div 
        class="card_area lg:w-[28%] cursor-pointer group" 
        @click="openPopup"
        role="button"
        tabindex="0"
        @keydown.enter="openPopup"
    >
        <div class="card_box rounded-2xl overflow-hidden w-full bg-white z-10 transition-transform duration-300 group-hover:shadow-xl">
            <div class="card_logo_area relative h-36 flex items-center justify-center p-4 bg-white">
                <img
                    :src="withBase(institutionData.logo)"
                    :class="['block max-w-[85%] object-contain m-auto pointer-events-none select-none', institutionData.logoClassName]"
                    alt="institution logo"
                />
            </div>
            <div class="card_img_area relative overflow-hidden h-56">
                <img
                    :src="withBase(institutionData.img)"
                    class="block w-full h-full object-cover object-center pointer-events-none select-none transition-transform duration-500 group-hover:scale-105"
                    alt="institution img"
                />
            </div>
        </div>
        <button 
            type="button" 
            @click.stop="openPopup" 
            class="more_btn block mx-auto -mt-6 z-40 relative cursor-pointer"
            aria-label="了解更多"
        >
            <img :src="withBase('/more.svg')" class="w-40 sm:w-44 h-auto pointer-events-none select-none" alt="了解更多" />
        </button>
    </div>
</template>

<style scoped>
   .card_box{
        box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.1); 
   }

   .more_btn{
        transition: transform .2s ease, filter .2s ease;
        filter: drop-shadow(0px 7px 15px rgba(0, 0, 0, 0.25));
        background: transparent;
        border: none;
        padding: 0;
        outline: none;
        -webkit-tap-highlight-color: transparent;
   }

   @media (hover: hover) {
       .more_btn:hover{
            transform: scale(1.08);
            filter: drop-shadow(0px 9px 18px rgba(0, 0, 0, 0.35));
       }
   }

   .more_btn:active{
        transform: scale(0.96);
   }

   .b0{ height: 75px; }
   .b1{ height: 65px; }
   .b2{ height: 55px; }
   .b3-half{ height: 50px; }
   .b3{ height: 45px; }
   .b4{ height: 35px; }
   .b5-half{ height: 30px; }
   .b5{ height: 25px; }
</style>
