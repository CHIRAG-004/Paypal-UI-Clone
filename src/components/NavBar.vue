<template>
  <div class="">
    <div v-if="showNav" class="flex mx-2 mt-3 justify-between text-[12px]">
      <div class="">
        <Button :text="'Menu'" :brCr="'border-[#0070ba]'" :txCr="'text-[#0070ba]'">
          <img :src="Menu" alt="menu" class="color-[#0070ba] w-5" />
        </Button>
      </div>
      <div>
        <img :src="Plogo" alt="" class="w-[25px] mt-1" />
      </div>
      <div>
        <Button :text="'Log in'" :brCr="'border-[#0070ba]'" :txCr="'text-[#0070ba]'" />
      </div>
    </div>
    <div v-else class="flex justify-between max-w-[1150px] mx-auto mt-5 px-7">
      <div>
        <router-link to="/"><img :src="Logo" alt="" class="w-[125px]" /></router-link>
      </div>
      <div class="flex gap-8 items-center font-medium text-[15px]">
        <div class="flex">
          <div>INDIVIDUAL</div>
          <div><img :src="Down" alt="" /></div>
        </div>
        <div class="flex">
          <div>BUSINESS</div>
          <div><img :src="Down" alt="" /></div>
        </div>
        <div class="flex">
          <div>PARTNERS</div>
          <div><img :src="Down" alt="" /></div>
        </div>
        <div class="flex">
          <div>USEFUL INFO</div>
          <div><img :src="Down" alt="" /></div>
        </div>
      </div>
      <div class="flex gap-1 text-[12px]">
        <Button :text="'Log in'" :brCr="'border-[#0070ba]'" :txCr="'text-[#0070ba]'" />
        <Button :text="'Sign Up'" class="bg-[#0070ba] text-white" />
      </div>
    </div>
    <div>

      <router-view/>
    </div>
  </div>
</template>

<script setup lang="ts">
import Plogo from "../assets/pLogo.webp";
import Down from "../assets/down.svg";
import Logo from "../assets/logo.svg";
import Button from "@/components/ButtonComp.vue";
import Menu from "../assets/menu.svg";
import { onMounted, onUnmounted, ref, watchEffect } from "vue";

const showNav = ref(false);
const width = ref(window.screen.width);

onMounted(() => {
  const event = () => {
    width.value = window.screen.width;
  };
  window.addEventListener("resize", event);
  onUnmounted(() => {
    window.removeEventListener("resize", event);
  });
});

watchEffect(() => {
  if (width.value < 1146) showNav.value = true;
  else showNav.value = false;
});
</script>

