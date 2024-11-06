<template>
  <div
    class="absolute bg-cover bg-[-800px] sm:bg-top w-full h-full text-white"
    :style="{ backgroundImage: `url(${props.image})` }"
    v-show="props.currentSlide == props.index"
  >
    <div class="bg-black/40 sm:bg-black/30 md:bg-black/20 xl:bg-black/0 w-full h-full ">
      <div class="pt-28 max-w-[1150px] xl:mx-auto mx-6">
        <div class="w-full xl:w-[47%]">
          <h1 class="font-bold text-[50px] leading-[50px]">
            {{ props.title }}
          </h1>
          <p class="text-balance text-[25px] w-fit mt-4 leading-8 font-medium">
            {{ props.content }}
          </p>
          <div class="flex mt-5 gap-2">
            <ButtonComp
              v-for="(btn, index) in props.btns"
              :key="index"
              :text="btn"
              :brCr="'border-white'"
              :txCr="'text-white'"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import ButtonComp from "./ButtonComp.vue";

const props = defineProps({
  image: String,
  index: Number,
  currentSlide: Number,
  title: String,
  content: String,
  btns: Array,
});
</script>
