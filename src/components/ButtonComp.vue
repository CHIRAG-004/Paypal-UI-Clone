<template>
  <button :class="[txCr, brCr, bgCr, 'border-[1px] rounded-3xl px-5 py-2 font-semibold flex gap-2 items-center']">
    <slot></slot>
    {{ props.text }}</button>
</template>

<script setup lang="ts">

const props = defineProps(["text", "brCr", "txCr", "bgCr"])


</script>
