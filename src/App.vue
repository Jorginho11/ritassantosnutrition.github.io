<template>
  <header class="bg-white fixed top-0 left-0 right-0 z-50 shadow-lg">
    <nav class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8" aria-label="Global">
      <div class="flex lg:flex-1">
        <a href="#" class="text-lg font-semibold text-gray-900">Age well with Rita</a>
      </div>
      <!-- Used for dropdown menu in small windows-->
      <div class="flex lg:hidden">
        <button type="button" class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700"
          @click="mobileMenuOpen = true">
          <span class="sr-only">Open main menu</span>
          <Bars3Icon class="size-6" aria-hidden="true" />
        </button>
      </div>
      <!-- Main page centered Menu-->
      <PopoverGroup class="hidden lg:flex lg:gap-x-10">
        <Popover class="relative">
          <PopoverButton class="flex items-center gap-x-1 text-sm/6 font-semibold text-gray-900">
            Home
            <ChevronDownIcon class="size-5 flex-none text-gray-400" aria-hidden="true" />
          </PopoverButton>

          <transition enter-active-class="transition ease-out duration-200" enter-from-class="opacity-0 translate-y-1"
            enter-to-class="opacity-100 translate-y-0" leave-active-class="transition ease-in duration-150"
            leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 translate-y-1">
            <PopoverPanel
              class="absolute top-full -left-8 z-10 mt-3 w-screen max-w-md overflow-hidden rounded-3xl bg-white ring-1 shadow-lg ring-gray-900/5">
              <div class="p-4">
                <div v-for="item in products" :key="item.name"
                  class="group relative flex items-center gap-x-6 rounded-lg p-4 text-sm/6 hover:bg-gray-50">
                  <div
                    class="flex size-11 flex-none items-center justify-center rounded-lg bg-gray-50 group-hover:bg-white">
                    <component :is="item.icon" class="size-6 text-gray-600 group-hover:text-indigo-600"
                      aria-hidden="true" />
                  </div>
                  <div class="flex-auto">
                    <a :href="item.href" class="block font-semibold text-gray-900">
                      {{ item.name }}
                      <span class="absolute inset-0" />
                    </a>
                    <p class="mt-1 text-gray-600">{{ item.description }}</p>
                  </div>
                </div>
              </div>
              <div class="grid grid-cols-2 divide-x divide-gray-900/5 bg-gray-50">
                <a v-for="item in callsToAction" :key="item.name" :href="item.href"
                  class="flex items-center justify-center gap-x-2.5 p-3 text-sm/6 font-semibold text-gray-900 hover:bg-gray-100">
                  <component :is="item.icon" class="size-5 flex-none text-gray-400" aria-hidden="true" />
                  {{ item.name }}
                </a>
              </div>
            </PopoverPanel>
          </transition>
        </Popover>

        <a href="#" class="text-sm/6 font-semibold text-gray-900">About me</a>
        <a href="#" class="text-sm/6 font-semibold text-gray-900">Services</a>
        <a href="#" class="text-sm/6 font-semibold text-gray-900">Research</a>
      </PopoverGroup>
      <div class="hidden lg:flex lg:flex-1 lg:justify-end">
        <a href="https://nutrium.com/p/ritasousasantos/schedule" class="text-sm/6 font-semibold text-gray-900">Schedule
          and Appointment <span aria-hidden="true">&rarr;</span></a>
      </div>
    </nav>
    <Dialog class="lg:hidden" @close="mobileMenuOpen = false" :open="mobileMenuOpen">
      <div class="fixed inset-0 z-10" />
      <DialogPanel
        class="fixed inset-y-0 right-0 z-10 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10">
        <div class="flex items-center justify-between">
          <a href="#" class="-m-1.5 p-1.5">
            <span class="sr-only">Your Company</span>
            <img class="h-8 w-auto" src="https://tailwindui.com/plus/img/logos/mark.svg?color=indigo&shade=600"
              alt="" />
          </a>
          <button type="button" class="-m-2.5 rounded-md p-2.5 text-gray-700" @click="mobileMenuOpen = false">
            <span class="sr-only">Close menu</span>
            <XMarkIcon class="size-6" aria-hidden="true" />
          </button>
        </div>
        <div class="mt-6 flow-root">
          <div class="-my-6 divide-y divide-gray-500/10">
            <div class="space-y-2 py-6">
              <Disclosure as="div" class="-mx-3" v-slot="{ open }">
                <DisclosureButton
                  class="flex w-full items-center justify-between rounded-lg py-2 pr-3.5 pl-3 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">
                  Product
                  <ChevronDownIcon :class="[open ? 'rotate-180' : '', 'size-5 flex-none']" aria-hidden="true" />
                </DisclosureButton>
                <DisclosurePanel class="mt-2 space-y-2">
                  <DisclosureButton v-for="item in [...products, ...callsToAction]" :key="item.name" as="a"
                    :href="item.href"
                    class="block rounded-lg py-2 pr-3 pl-6 text-sm/7 font-semibold text-gray-900 hover:bg-gray-50">{{
                    item.name }}</DisclosureButton>
                </DisclosurePanel>
              </Disclosure>
              <a href="#"
                class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">Features</a>
              <a href="#"
                class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">Marketplace</a>
              <a href="#"
                class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">Company</a>
            </div>

          </div>
        </div>
      </DialogPanel>
    </Dialog>
  </header>

  <div class="container mx-auto px-4 py-8 pt-30">
    <div class="grid grid-cols-2 gap-8">
      <!-- Left column -->
      <div class="bg-gray-50 p-6 rounded-lg">
        <h2 class="text-xl font-bold mb-4">About Me</h2>
        <p class="text-gray-700">
          Hi! I'm Rita Santos, a registered nutritionist dedicated to helping you achieve your health goals.
          With expertise in personalized nutrition plans and lifestyle modifications,
          I can guide you towards a healthier and more balanced life.
        </p>
      </div>

      <!-- Right column -->
      <div class="bg-gray-50 p-6 rounded-lg">
        <h2 class="text-xl font-bold mb-4">My Services</h2>
        <ul class="list-disc list-inside text-gray-700">
          <li>Personalized Nutrition Plans</li>
          <li>Weight Management</li>
          <li>Sports Nutrition</li>
          <li>Dietary Consultations</li>
          <li>Meal Planning</li>
        </ul>
      </div>
    </div>
  </div>
  <!-- Image Gallery -->
  <div class="container mx-auto py-8 px-4">
    <h2 class="text-3xl font-semibold text-center mb-6">Galeria</h2>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 justify-items-center">
      <div class="w-full max-w-sm aspect-square">
        <img src="./images/tile_1.png" alt="Image 1" class="w-full h-full object-cover rounded-lg shadow-lg" />
      </div>
      <div class="w-full max-w-sm aspect-square">
        <img src="./images/tile_2.jpg" alt="Image 2" class="w-full h-full object-cover rounded-lg shadow-lg" />
      </div>
      <div class="w-full max-w-sm aspect-square">
        <img src="./images/tile_3.jpg" alt="Image 3" class="w-full h-full object-cover rounded-lg shadow-lg" />
      </div>
    </div>
  </div>
  <!-- Socials Footer -->
  <footer class="bg-gray-800 text-white py-12">
    <div class="container mx-auto px-4">
      <div class="flex justify-center space-x-8">
        <a href="https://twitter.com" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fab fa-twitter text-2xl hover:text-blue-400"></i>
        </a>
        <a href="https://facebook.com" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fab fa-facebook text-2xl hover:text-blue-600"></i>
        </a>
        <a href="https://instagram.com" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fab fa-instagram text-2xl hover:text-pink-600"></i>
        </a>
        <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fab fa-linkedin text-2xl hover:text-blue-400"></i>
        </a>
        <a href="https://youtube.com" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fab fa-youtube text-2xl hover:text-red-600"></i>
        </a>
        <a href="mailto:contact@example.com" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fas fa-envelope text-2xl hover:text-gray-400"></i>
        </a>
        <a href="https://wa.me/1234567890" target="_blank" rel="noopener noreferrer"
          class="transform transition-transform hover:scale-110">
          <i class="fab fa-whatsapp text-2xl hover:text-green-400"></i>
        </a>
      </div>
      <p class="mt-8 text-center text-sm">© 2024 Age Well with Rita. All rights reserved.</p>
    </div>
  </footer>
</template>

<script setup>
import { ref } from 'vue'
import {
  Dialog,
  DialogPanel,
  Disclosure,
  DisclosureButton,
  DisclosurePanel,
  Popover,
  PopoverButton,
  PopoverGroup,
  PopoverPanel,
} from '@headlessui/vue'
import {
  ArrowPathIcon,
  Bars3Icon,
  ChartPieIcon,
  CursorArrowRaysIcon,
  FingerPrintIcon,
  SquaresPlusIcon,
  XMarkIcon,
} from '@heroicons/vue/24/outline'
import { ChevronDownIcon, PhoneIcon, PlayCircleIcon } from '@heroicons/vue/20/solid'

const products = [
  { name: 'Schedule an Appointment', description: '', href: 'https://nutrium.com/p/ritasousasantos/schedule', icon: ChartPieIcon },
]
const callsToAction = [
  { name: 'Watch demo', href: '#', icon: PlayCircleIcon },
  { name: 'Contact sales', href: '#', icon: PhoneIcon },
]

const mobileMenuOpen = ref(false)
</script>