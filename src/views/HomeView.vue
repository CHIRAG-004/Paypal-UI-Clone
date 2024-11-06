<script setup lang="ts">
import { onBeforeUnmount, onMounted, reactive, ref } from "vue";
import Image1 from "../assets/image1.jpg";
import Image2 from "../assets/image2.jpg";
import CarouselItem from "@/components/CarouselItem.vue";
import ButtonComp from "@/components/ButtonComp.vue";
import Arrow from "../assets/arrow.svg";
// import ButtonComp from "@/components/ButtonComp.vue";

const images = reactive([
  {
    img: Image1,
    title: "Secure payments. Smooth shopping.",
    content:
      "More ways to pay and more places to shop. Send money quickly and easily around the globe.",
    btns: ["Sign Up"],
  },
  {
    img: Image2,
    title: "Sell just about anywhere in the world.",
    content:
      "Whether you have an online shop or need to accept payments remotely, we can help you get paid fast.",
    btns: ["Sign up", "Connect With Us"],
  },
]);

const SlideInterval = ref<number | undefined | ReturnType<typeof setInterval>>(
  undefined
);
const currentSlide = ref(1);

onMounted(() => {
  SlideInterval.value = setInterval(() => {
    currentSlide.value = (currentSlide.value + 1) % 2;
  }, 5000);
});

onBeforeUnmount(() => {
  if (SlideInterval.value !== undefined) {
    clearInterval(SlideInterval.value);
  }
});
</script>

<template>
  <main>
    <div class="mt-5">
      <div
        class="relative overflow-hidden h-[650px] sm:h-[480px] bg-blue-300 w-full"
      >
        <CarouselItem
          v-for="(image, index) in images"
          :key="index"
          :image="image.img"
          :index="index"
          :currentSlide="currentSlide"
          :title="image.title"
          :content="image.content"
          :btns="image.btns"
        />
        <div
          class="absolute mt-[200px] flex w-full pt-[390px] sm:pt-[200px] xl:pt-0"
        >
          <img
            :src="Arrow"
            alt=""
            class="absolute rotate-180 w-14 cursor-pointer"
            :class="{ 'opacity-50 cursor-auto': currentSlide == 0 }"
            @click="currentSlide = 0"
          />
          <img
            :src="Arrow"
            alt=""
            class="absolute w-14 right-0 cursor-pointer"
            @click="currentSlide = 1"
            :class="{ 'opacity-50 cursor-auto': currentSlide == 1 }"
          />
        </div>
        <div
          class="absolute text-white flex gap-2 justify-center w-full bottom-2"
        >
          <span
            class="bg-white w-4 rounded-full h-4 hover:bg-blue-500 cursor-pointer"
            @click="currentSlide = 0"
            :class="{ 'opacity-50 hover:bg-white/100 cursor-auto': currentSlide == 0 }"
          ></span>
          <span
            class="bg-white w-4 rounded-full h-4 hover:bg-blue-500 cursor-pointer"
            @click="currentSlide = 1"
            :class="{ 'opacity-50 hover:bg-white/100 cursor-auto': currentSlide == 1 }"
          ></span>
        </div>
      </div>
    </div>
    <div class="bg-[#001535] text-white flex justify-center">
      <div
        class="flex flex-col gap-3 xl:flex-row w-[1150px] justify-between items-center py-11 px-6"
      >
        <div class="leading-8">
          <h3 class="text-[25px] font-bold">
            Looking for PayPal Business Solutions?
          </h3>
          <p class="text-[22px] font-medium">
            Across regions and around the world, we are here to support you.
          </p>
        </div>
        <div>
          <ButtonComp
            :text="'PayPal for business'"
            :txCr="'text-white'"
            :bgCr="'bg-[#0070ba]'"
            :brCr="'border-[#0070ba]'"
          />
        </div>
      </div>
    </div>
  </main>
</template>
