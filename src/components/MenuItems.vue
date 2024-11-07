<template>
  <div>
    <div class="min-h-screen w-[65%] bg-[#0a2962] absolute z-20 text-white">
      <div class="mt-7 mx-4">
        <div class="flex items-center gap-3" @click="hideMenu">
          <img :src="Arrow" alt="" class="rotate-180 h-[15px] opacity-80" />
          <h1 class="font-bold text-[20px]">{{ props.data.title }}</h1>
        </div>
        <div class="">
          <div v-for="(item, index) in props.data.content" :key="index" class="mt-3">
            <div class="font-thin text-[15px]">{{ item.title }}</div>
            <hr v-if="item.title" class="opacity-60 mt-2">
            <div v-for="(items, ind) in item.subtitle" :key="ind" class="mt-3 ml-3 text-[15px]" :class="{'mt-6': !item.title}">{{ items }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import Arrow from "../assets/arrow.svg";

const props = defineProps(["data"]);
const emit = defineEmits<{ (e: "updateMenu", value: boolean): void }>();

function hideMenu() {
  emit("updateMenu", false)
}

</script>

<style>
</style>
