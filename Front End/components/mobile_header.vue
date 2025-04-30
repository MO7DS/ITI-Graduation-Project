<template>
    <div class="block lg:hidden">
      <button
        @click="toggleMobileMenu"
        class="text-[#A31D1D]  text-3xl focus:outline-none cursor-pointer"
      >
        <i class="fas fa-bars"></i>
      </button>

      <div
      :class="isMobileMenuOpen ? 'translate-x-0 opacity-100' : 'translate-x-full opacity-0 pointer-events-none'"
   
   class="fixed top-0 flex flex-col justify-between right-0 mt-2 w-60 h-screen bg-orange-50 shadow-lg rounded-xl transition-all duration-500 ease-in-out transform
     border border-red-200 z-50 p-4 space-y-4"
        
      >

      
        <div class="flex flex-col gap-10 items-start">
          <button
        @click="toggleMobileMenu"
        class="text-[#A31D1D] px-3  text-3xl focus:outline-none cursor-pointer"
      >
        <i class="fas fa-bars"></i>
          </button>

          <div class="flex flex-col gap-4">
            <div v-if="isAuthenticated" class="flex flex-col gap-2">
              <NuxtLink
                to="/profile"
                @click="closeMobileMenu"
                class=" font-medium hover:underline px-3 py-2.5"
              >
                <p class="text-black text-lg font-medium">Hello, </p>
                <p class="text-red-900 font-bold text-xl" >{{ authStore.user.name }}</p>
              </NuxtLink>
            </div>
            <!-- Home -->
            <NuxtLink
              to="/"
              class="flex items-center gap-2 px-3 py-2.5 text-xl text-red-900 transition-all duration-300 hover:rounded-full hover:bg-orange-100 hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
              @click="closeMobileMenu"
              :class="route.path === '/' ? 'font-bold border-b-[2px] border-red-900' : 'font-semibold'"
            >
            <div class="relative w-8 h-7 flex items-center justify-center">
            <img
            v-if="route.path === '/'"
            src="../assets/home-fill.svg"
            class="w-8 h-8"
          />
          <img v-else src="../assets/home-stroke.svg" class="w-8 h-8" />
        </div>
              <span 
                >Home</span
              >
            </NuxtLink>

            <!-- Marketplace -->
            <NuxtLink
              to="/market"
              class="relative flex items-center gap-2 px-3 py-2.5 cursor-pointer text-red-900 transition-all duration-300 hover:rounded-full hover:bg-orange-100 hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
              @click="closeMobileMenu"
              :class="
                  route.path === '/market'
                    ? 'font-bold border-b-[2px] border-red-900'
                    : 'font-semibold'
                "
            >
              <div class="relative w-8 h-7 flex items-center justify-center">
                <img
                  v-if="route.path !== '/market'"
                  src="../assets/store-stroke.svg"
                  class="w-8 h-8"
                />
                <img v-else src="../assets/store-fill.svg" class="w-8 h-8" />
              </div>

              <span
               class=" text-xl"
                >Marketplace</span
              >
            </NuxtLink>

            <!-- Favorite -->
            <NuxtLink
              :to="isAuthenticated ? '/favorite' : '/login'"
              @click="closeMobileMenu"
              :class="[
                'relative flex items-center cursor-pointer group px-4 py-2.5 transition-all duration-300 hover:rounded-full hover:bg-orange-100 hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]',
                route.path === '/favorite'
                  ? 'border-b-[2px] border-red-900'
                  : '',
              ]"
            >
              <div class="relative w-8 h-7 flex items-center justify-center">
                <i
                  :class="[
                    'relative text-2xl text-red-900 mr-3',
                    route.path === '/favorite'
                      ? 'fa-solid fa-heart fill'
                      : 'fa-regular fa-heart fill',
                  ]"
                >
                  <span
                    v-if="wishlistCount > 0"
                    class="absolute -top-3 -right-3 bg-red-800 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center"
                  >
                    {{ wishlistCount }}
                  </span>
                </i>
              </div>

              <p
                :class="[
                  'text-red-900 text-xl ',
                  route.path === '/favorite' ? 'font-bold' : 'font-semibold',
                ]"
              >
                Favorite
              </p>
            </NuxtLink>

            <!-- Cart -->
            <NuxtLink
              :to="isAuthenticated ? '/cart' : '/login'"
              class="flex items-center gap-2 px-3 py-2.5 text-red-900 text-xl transition-all duration-300 hover:rounded-full hover:bg-orange-100 hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
              @click="closeMobileMenu"
              :class="route.path === '/cart' ? 'font-bold border-b-[2px] border-red-900' : 'font-semibold'"
            >
            <div class="relative w-8 h-7 flex items-center justify-center">
              <img
              v-if="route.path !== '/cart'"
              src="../assets/cart-shopping.svg"
              class="w-6 h-6"
            />
            <img
              v-else
              src="../assets/cart-shopping-solid.svg"
              class="w-6 h-6"
            />
            <span
                v-if="cartItemCount > 0"
                class="absolute -top-3 -right-3 bg-[#A31D1D] text-white text-xs rounded-full w-5 h-5 flex items-center justify-center"
              >
                {{ cartItemCount }}
              </span>
              </div>
             

              <span
                
                >Cart</span
              >
            </NuxtLink>
          </div>
          <!-- Auth Buttons -->
          <div v-if="!isAuthenticated" class="flex flex-col gap-3 w-full">
            <NuxtLink
              to="/login"
              @click="closeMobileMenu"
              class="text-stone-900  px-6 py-1.5 bg-white font-medium text-lg flex itms-center justify-center"
            >
              Log in
            </NuxtLink>
            <NuxtLink
              to="/sign-up"
              @click="closeMobileMenu"
              class="text-red-200 font-medium text-lg px-6 py-1.5 bg-red-900 rounded-2xl flex itms-center justify-center"
            >
              Sign up
            </NuxtLink>
          </div>
        </div>

        <button
        v-if="isAuthenticated"
        @click="handleLogout"
        class="block w-full text-left py-2.5 px-4 text-[#A31D1D] font-semibold text-xl transition-all duration-300 hover:rounded-full hover:bg-orange-100 hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]"
      >
        <i class="fa-solid fa-right-from-bracket rotate-180 mr-2"></i> Logout
      </button>
      </div>
    </div>
</template>
<script setup>
import { useAuthStore } from '~/stores/auth';
import { NuxtLink } from '#components';
import { useAuth } from '~/composables/useAuth';

import { computed, ref } from "vue";
import { useCartStore } from "~/stores/cart";
import { useWishlistStore } from "~/stores/wishlist";
const wishlistStore = useWishlistStore();

const wishlistCount = computed(() => wishlistStore.items.length);

const authStore = useAuthStore();
const cartStore = useCartStore();
const { logout } = useAuth();
const route = useRoute();

const isAuthenticated = computed(() => authStore.isAuthenticated);
const cartItemCount = computed(() => cartStore.totalItems);

const isMobileMenuOpen = ref(false);

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false;
};

const baseClasses = `px-3.5 py-2 flex justify-center items-center gap-1 transition-all duration-300 hover:bg-orange-100 hover:rounded-full hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)]`;
const hoverClasses = `border-b-[2px] border-red-800 hover:bg-orange-100 hover:rounded-full hover:shadow-[0px_0px_4px_0px_rgba(0,0,0,0.50)] `;





const handleLogout = () => {
  logout();
};
</script>