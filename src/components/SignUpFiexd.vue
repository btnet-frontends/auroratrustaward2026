<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { withBase } from '../utils/utils'

const show = ref(false);


function handleScroll() {
  show.value = window.scrollY > 200
}

function goToSignUp() {
    const el = document.getElementById('signUp')
    if (el) {
        el.scrollIntoView({ behavior: 'smooth' })
    }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
});
</script>

<template>
  <div class="fixed bottom-[5%] right-3 sm:right-4 z-52 w-fit flex flex-col items-center gap-2 md:gap-3 lg:gap-4 md:bottom-[20%] lg:bottom-[25%]">
    <a :href="withBase('/SignUp')" class="signUp_fixed_btn hover:scale-105 transition-transform duration-200">
        <img :src="withBase('/fixed_btn1.svg')" class="fixed_btn_img" alt="sign up btn img">
    </a>

    <a :href="withBase('/SignUpAlready')" class="signUp_fixed_btn hover:scale-105 transition-transform duration-200">
        <img :src="withBase('/fixed_btn2.svg')" class="fixed_btn_img" alt="sign up btn img">
    </a>

    <a :href="withBase('/SignUpInstitution')" class="signUp_fixed_btn hover:scale-105 transition-transform duration-200">
        <img :src="withBase('/fixed_btn3.svg')" class="fixed_btn_img" alt="sign up btn img">
    </a>
  </div>
</template>

<style scoped>
.fixed_btn_img {
  width: 68px;
  display: block;
}

@media (min-width: 640px) {
  .fixed_btn_img {
    width: 78px;
  }
}

@media (min-width: 768px) {
  .fixed_btn_img {
    width: 95px;
  }
}

@media (min-width: 1024px) {
  .fixed_btn_img {
    width: 108px;
  }
}

@media (min-width: 1280px) {
  .fixed_btn_img {
    width: 115px;
  }
}

@media (min-width: 1536px) {
  .fixed_btn_img {
    width: 120px;
  }
}
</style>