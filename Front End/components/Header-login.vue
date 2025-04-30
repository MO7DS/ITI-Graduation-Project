<template>
  <header
    class="flex py-[16px] px-[24px] justify-between items-center relative"
  >
    <!-- Hidden on mobile -->
    <NuxtLink to="/market" class="hidden lg:block">
      <div
        class="text-center flex justify-start text-red-900 text-lg font-medium leading-relaxed"
      >
        Explore Marketplace
      </div>
    </NuxtLink>

    <!-- Logo -->
    <NuxtLink to="/">
      <div
        class="text-black text-center text-[20px] not-italic font-bold leading-[30px] tracking-[-0.38px]"
      >
        <img src="../Logo.svg" />
      </div>
    </NuxtLink>

    <!-- Desktop Buttons Hidden on mobile) -->
    <div class="hidden lg:flex items-center justify-center gap-[10px]">
      <!-- Profile Button -->
      <NuxtLink
        to="/profile"
        class="px-[8px] py-[5px] flex flex-col items-center justify-center transition-all duration-300"
      >
        <div v-if="!authStore?.user" class="flex items-center justify-center">
          <i class="fa-solid fa-spinner animate-spin text-[#A31D1D]"></i>
        </div>
        <div v-else>
          <p class="text-black text-xs font-medium">Hello</p>
          <p class="text-red-800 text-xs font-extrabold">
            {{ authStore.user.name }}
          </p>
        </div>
      </NuxtLink>

      <!-- Logout Button -->
      <button
        @click="handleLogout"
        class="p-[8px] px-[12px] text-[#A31D1D] text-center font-[Poppins] text-[20px] font-medium leading-[150%] tracking-[-0.304px] cursor-pointer transition-all duration-300 hover:bg-orange-100 hover:rounded-full hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
      >
        <i class="fa-solid fa-right-from-bracket rotate-180"></i>
      </button>
    </div>

    <MobileHeader />
  </header>
</template>

<script setup>
import { useAuthStore } from "~/stores/auth";
import { NuxtLink } from "#components";
import { useAuth } from "~/composables/useAuth";

const authStore = useAuthStore();
const { logout } = useAuth();

const handleLogout = () => {
  logout();
};
</script>
