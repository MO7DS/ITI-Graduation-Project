
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

    <!-- Desktop Buttons Hidden on mobile -->
    <div class="hidden lg:flex items-center justify-center gap-[10px]">
      <div
        v-if="!isAuthenticated"
        class="flex items-center justify-center gap-[10px]"
      >
        <!-- Log in Button -->
        <NuxtLink to="login">
          <button
            class="p-[12px] px-[14px] text-[#A31D1D] text-center text-[20px] font-medium leading-[150%] tracking-[-0.304px] cursor-pointer transition-all duration-300 hover:bg-orange-100 hover:rounded-full hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
          >
            Log in
          </button>
        </NuxtLink>

        <!-- Sign up Button -->
        <NuxtLink to="sign-up">
          <button
            class="p-[10px] px-[24px] rounded-[16px] bg-[#A31D1D] shadow-[0px_0px_4px_rgba(0,0,0,0.50)] text-[#ECDCBF] text-center text-[20px] font-medium leading-[150%] tracking-[-0.304px] cursor-pointer transition duration-300 ease-in-out py-3 hover:bg-[#6D1313] hover:shadow-lg hover:rounded-[50px]"
          >
            Sign up
          </button>
        </NuxtLink>
      </div>

      <div v-else class="flex items-center space-x-4">
        <button
          @click="handleLogout"
          class="p-[8px] px-[12px] text-[#A31D1D] text-center text-[20px] font-medium leading-[150%] tracking-[-0.304px] cursor-pointer transition-all duration-300 hover:bg-orange-100 hover:rounded-full hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
        >
          <i class="fa-solid fa-right-from-bracket rotate-180"></i>
        </button>
      </div>
    </div>

    <!-- mobile -->
    <MobileHeader />
  </header>
</template>

<script setup>
import { useAuthStore } from "~/stores/auth";
import { NuxtLink } from "#components";
import { useAuth } from "~/composables/useAuth";

import { computed, ref } from "vue";

const authStore = useAuthStore();
const { logout } = useAuth();

const isAuthenticated = computed(() => authStore.isAuthenticated);

const handleLogout = () => {
  logout();
};
</script>
