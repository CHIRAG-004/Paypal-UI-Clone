<template>
  <div class="fixed top-0 z-30 w-full bg-white pb-1">
    <div v-if="showNav" class="flex mx-2 mt-3 justify-between text-[12px]">
      <div>
        <Button
          :text="'Menu'"
          :brCr="'border-[#0070ba]'"
          :txCr="'text-[#0070ba]'"
          @click="manageMenu"
        >
          <img :src="showMenu ? Close : Menu" alt="" class="w-5" />
        </Button>
      </div>
      <div>
        <img :src="Plogo" alt="PLogo" class="w-[25px] mt-1" />
      </div>
      <div>
        <Button
          :text="'Log in'"
          :brCr="'border-[#0070ba]'"
          :txCr="'text-[#0070ba]'"
        />
      </div>
    </div>

    <div v-else class="flex justify-between max-w-[1150px] mx-auto mt-5 px-7">
      <div>
        <router-link to="/" :showMenu="showMenu"
          ><img :src="Logo" alt="Logo" class="w-[125px]"
        /></router-link>
      </div>
      <div class="flex gap-8 items-center font-medium text-[15px]">
        <div
          v-for="(item, index) in navItems"
          :key="index"
          class="flex items-center gap-1"
        >
          <div>{{ item }}</div>
          <img :src="Down" alt="Dropdown Icon" class="w-4 h-4" />
        </div>
      </div>
      <div class="flex gap-1 text-[12px]">
        <Button
          :text="'Log in'"
          :brCr="'border-[#0070ba]'"
          :txCr="'text-[#0070ba]'"
        />
        <Button :text="'Sign Up'" class="bg-[#0070ba] text-white" />
      </div>
    </div>
  </div>

  <div>
    <div class="h-screen w-[65%] bg-[#0a2962] absolute z-10" v-if="showMenu && showNav">
      <div class="mt-6 mx-4">
        <div
          v-for="(item, index) in navItems"
          :key="index"
          class="flex text-white text-[15px] items-center gap-2 mt-4 cursor-pointer"
          @click="manageMenuItems(index)"
        >
          <h1 class="font-medium">{{ item }}</h1>
          <img :src="Arrow" alt="" class="h-[15px] opacity-80" />
        </div>
        <hr class="bg-white mt-4 opacity-65" />

        <div>
          <Button
            :text="'Sign Up'"
            :tx-cr="'text-white'"
            class="mt-[550px] mx-auto flex justify-center w-[70%] font-normal"
          />
        </div>
      </div>
    </div>

    <div v-if="showMenuItems">
      <MenuItems :data="menuData[index]" @updateMenu="showMenuItems = $event" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, watchEffect, reactive } from "vue";
import Plogo from "../assets/pLogo.webp";
import Down from "../assets/down.svg";
import Logo from "../assets/logo.svg";
import Button from "@/components/ButtonComp.vue";
import Menu from "../assets/menu.svg";
import Close from "../assets/close.svg";
import Arrow from "../assets/arrow.svg";
import MenuItems from "./MenuItems.vue";

const showNav = ref(false);
const width = ref(window.innerWidth);
const showMenu = ref(false);
const navItems = ref(["INDIVIDUAL", "BUSINESS", "PARTNERS", "USEFUL INFO"]);
const showMenuItems = ref(false);
const index = ref(0);

const menuData = reactive([
  {
    title: navItems.value[0],
    content: [
      {
        title: "",
        subtitle: [
          "Individual Home",
          "Buyer Protection",
          "Shop with Paypal",
          "Getting Started",
        ],
      },
    ],
  },
  {
    title: navItems.value[1],
    content: [
      {
        title: "SMALL-TO-MEDIUM BUSINESS",
        subtitle: [
          "Introdunction",
          "Getting Started",
          "Solution",
          "Accept Payments",
          "Make Payments",
          "Manage Risk",
          "Accelerate Growth",
          "Streamine Operations",
        ],
      },
      {
        title: "ENTERPRISE",
        subtitle: [
          "Introduction",
          "Marketplaces & Partners",
          "Platform & Solutions",
          "Accept Payments",
          "Make Payments",
          "Manage Risk",
          "Accelerate Growth",
          "Streamline Operations",
        ],
      },
      {
        title: "MORE",
        subtitle: [
          "Pricing",
          "Business Resource Center",
          "Identity Verifications (KYC)",
        ],
      },
    ],
  },
  {
    title: navItems.value[2],
    content: [
      { title: "", subtitle: ["Partner With Us", "Partner Directory"] },
    ],
  },
  {
    title: navItems.value[3],
    content: [
      {
        title: "",
        subtitle: [
          "Online Security",
          "Fraud Prevention",
          "Phising",
          "PCI Compliance",
          "Foreign Inward Remittamce Advise (FIRA)",
          "Help Center",
        ],
      },
    ],
  },
]);

function manageMenu() {
  showMenu.value = !showMenu.value;
  showMenuItems.value = false;
}

function manageMenuItems(ind: number) {
  showMenuItems.value = true;
  index.value = ind;
}

onMounted(() => {
  const updateWidth = () => {
    width.value = window.innerWidth;
  };
  window.addEventListener("resize", updateWidth);

  if (width.value < 1146) showNav.value = true;

  onUnmounted(() => {
    window.removeEventListener("resize", updateWidth);
  });
});

watchEffect(() => {
  showNav.value = width.value < 1146;
});
</script>

