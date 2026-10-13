<script setup>
    import { withBase } from '../utils/utils'
    import { onMounted, onUnmounted } from 'vue'
    
    const props = defineProps({
        institutionData: Object
    });

    const emit = defineEmits(['close']);

    function handleKeyDown(e) {
        if (e.key === 'Escape') {
            emit('close');
        }
    }

    onMounted(() => {
        window.addEventListener('keydown', handleKeyDown);
        if (typeof document !== 'undefined') {
            document.body.style.overflow = 'hidden';
        }
    });

    onUnmounted(() => {
        window.removeEventListener('keydown', handleKeyDown);
        if (typeof document !== 'undefined') {
            document.body.style.overflow = '';
        }
    });
</script>

<template>
    <Teleport to="body">
        <div 
          class="popUpBox_area fixed inset-0 p-4 sm:p-6 flex justify-center items-center w-full h-full" 
          style="background-color: rgba(0,0,0,.5); z-index: 99999;"
          @click.self="emit('close')"
        >
            <div class="popUp_box relative rounded-2xl overflow-hidden p-5 sm:p-8 w-full max-w-lg md:max-w-2xl lg:max-w-3xl max-h-[90vh] flex flex-col bg-white">
                <div class="popUp_head relative shrink-0">
                    <button 
                        type="button" 
                        class="close_btn absolute right-0 top-0 cursor-pointer text-3xl sm:text-4xl text-neutral-500 hover:text-neutral-800 p-1 leading-none" 
                        @click="emit('close')"
                        aria-label="關閉"
                    >
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                    <div class="flex flex-col items-center gap-3 pt-6 pb-2">
                        <img
                            v-if="props.institutionData?.logo"
                            :src="withBase(props.institutionData.logo)"
                            :class="['h-14 sm:h-16 mb-2 object-contain', props.institutionData.logoClassName]"
                            alt="institution logo"
                        />
                    </div>
                </div>
                <div class="popUp_body overflow-y-auto py-3 px-1 my-2">
                    <p class="text-base sm:text-lg text-justify leading-7 whitespace-pre-line text-neutral-700" v-html="props.institutionData?.description"></p>
                </div>
                <div class="popUp_footer shrink-0 pt-2 pb-1">
                    <a 
                      v-if="props.institutionData?.url"
                      :href="props.institutionData.url" 
                      target="_blank" 
                      rel="noopener" 
                      class="goToArticle_btn w-fit block mx-auto px-8 py-2.5 rounded-full shadow-md" 
                      style="background-color: #E03127;"
                    >
                        <p class="text-white text-lg sm:text-xl font-medium">觀看文章</p>
                    </a>
                </div>
            </div>
        </div>
    </Teleport>
</template>

<style scoped>
   .popUp_box{
        box-shadow: 0px 8px 30px rgba(0, 0, 0, 0.25); 
   }

   .close_btn{
        transition: transform .2s ease;
        background: transparent;
        border: none;
   }

   .close_btn:hover{
        transform: scale(1.15);
   }

   .goToArticle_btn{
        transition: transform .2s ease, filter .2s ease;
   }

   .goToArticle_btn:hover{
        transform: scale(1.05);
   }

   .b0{ height: 85px; }
   .b1{ height: 75px; }
   .b2{ height: 65px; }
   .b3-half{ height: 60px; }
   .b3{ height: 55px; }
   .b4{ height: 45px; }
   .b5-half{ height: 40px; }
   .b5{ height: 35px; }
</style>
