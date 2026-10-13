<script setup>

    import { ref, onMounted } from 'vue'
    
    import Title from './Title.vue'
    import Card from './Card.vue'
    import PopUpBox from './PopUpBox.vue'

    import AOS from 'aos'
    import 'aos/dist/aos.css'
    

    defineProps(
        {
            infoData: Object
        }
    );

    const popupOpen = ref(false)
    const selectedInstitution = ref(null)

    const openPopup = (item) => {
        selectedInstitution.value = item
        popupOpen.value = true
    }

    const closePopup = () => {
        popupOpen.value = false
        // keep selectedInstitution for potential reuse; clear if needed
        // selectedInstitution.value = null
    }

    onMounted(() => {
        AOS.init()
    });


</script>

<template>
    <div class="content_wrap institution_wrap z-10">
        <Title :infoData="infoData" />
        <div class="institution_box py-10 px-10 sm:px-20 mx-5 xl:mx-auto pb-12" data-aos="fade-up" data-aos-delay="500" data-aos-duration="1000">
           <div class="card_box w-full flex flex-wrap justify-center gap-20">
             <Card 
               v-for="(item ,idx) in infoData.institution" 
               :key="idx" 
               :institutionData="item"
               @show-popup="openPopup"
             />
           </div>
        </div>
    </div>
    <PopUpBox 
      v-if="popupOpen" 
      :institutionData="selectedInstitution" 
      @close="closePopup" 
    />
</template>

<style scoped lang="scss">
    .institution_wrap {
        padding-bottom: 220px !important;
    }

    @media screen and (max-width: 1024px) {
        .institution_wrap {
            padding-bottom: 160px !important;
        }
    }
    @media screen and (max-width: 768px) {
        .institution_wrap {
            padding-bottom: 120px !important;
        }
    }
</style>
