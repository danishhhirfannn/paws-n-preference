<script setup>
import Card from '@/volt/Card.vue'
import Button from '@/volt/Button.vue'
import { ref, computed, nextTick } from 'vue'
import { DotLottieVue } from '@lottiefiles/dotlottie-vue'

// Sample carousel data with different images
const carouselItems = ref([
    {
        id: 1,
        image: 'https://primefaces.org/cdn/primevue/images/card-vue.jpg',
        title: 'Card 1'
    },
    {
        id: 2,
        image: 'https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=400&h=300&fit=crop',
        title: 'Card 2'
    },
    {
        id: 3,
        image: 'https://images.unsplash.com/photo-1441974231531-c6227db76b6e?w=400&h=300&fit=crop',
        title: 'Card 3'
    }
])

const currentIndex = ref(0)

const next = () => {
    currentIndex.value = (currentIndex.value + 1) % carouselItems.value.length
}

const prev = () => {
    currentIndex.value = currentIndex.value === 0
        ? carouselItems.value.length - 1
        : currentIndex.value - 1
}

const getCurrentImage = computed(() => {
    return carouselItems.value[currentIndex.value].image
})

const getPrevImage = computed(() => {
    const prevIndex = currentIndex.value === 0 ? carouselItems.value.length - 1 : currentIndex.value - 1
    return carouselItems.value[prevIndex].image
})

const getNextImage = computed(() => {
    const nextIndex = (currentIndex.value + 1) % carouselItems.value.length
    return carouselItems.value[nextIndex].image
})

const lottieRef = ref(null)
const showAnimation = ref(false)

function handleClickAnimation() {
  showAnimation.value = true
  nextTick(() => lottieRef.value?.getDotLottieInstance()?.play())

  setTimeout(() => {
    showAnimation.value = false
  }, 2000)   // adjust to taste
}

const heartLottieRef = ref(null)
const showHeartAnim = ref(false)

function handleHeartClick() {
  showHeartAnim.value = true
  nextTick(() => heartLottieRef.value?.getDotLottieInstance()?.play())

  setTimeout(() => {
    showHeartAnim.value = false
  }, 2000)
}
</script>

<template>
    <div class="flex flex-col items-center flex-1 pb-6 relative">
        <!-- Floating Lottie Animation -->
        <Transition
            enter-active-class="transition-all duration-500 ease-out"
            enter-from-class="opacity-0 scale-75 transform translate-y-4"
            enter-to-class="opacity-100 scale-100 transform translate-y-0"
            leave-active-class="transition-all duration-300 ease-in"
            leave-from-class="opacity-100 scale-100 transform translate-y-0"
            leave-to-class="opacity-0 scale-75 transform translate-y-4"
        >
            <div
                v-show="showAnimation"
                class="absolute top-65 right-26 z-30 bg-white rounded-full p-10 shadow-lg"
            >
                <DotLottieVue
                    ref="lottieRef"
                    style="height: 150px; width: 150px"
                    src="https://lottie.host/f8b68722-cd5d-44ec-b6e4-a59d2f0536f2/V9jFCwiWSb.lottie"
                />
            </div>
        </Transition>
        <!-- Floating Lottie Animation -->
        <Transition
        enter-active-class="transition-all duration-500 ease-out"
        enter-from-class="opacity-0 scale-75 transform translate-y-4"
        enter-to-class="opacity-100 scale-100 transform translate-y-0"
        leave-active-class="transition-all duration-300 ease-in"
        leave-from-class="opacity-100 scale-100 transform translate-y-0"
        leave-to-class="opacity-0 scale-75 transform translate-y-4"
        >
        <!-- ❤️ heart animation (no bg wrapper) -->
        <div
            v-show="showHeartAnim"
            class="absolute top-65 z-30"
        >
            <DotLottieVue
            ref="heartLottieRef"
            style="height: 300px; width: 500px"
            src="https://lottie.host/297688bd-0713-484a-8774-19c1a575773c/QQQDZX0ZyI.lottie"
            />
        </div>
        </Transition>

        <!-- Vertical Carousel Container -->
        <div class="relative w-full h-full flex items-center justify-center overflow-hidden">
            <!-- Previous Card (Left) -->
            <div class="absolute left-3 lg:left-140 opacity-60">
                <Card
                    class="w-96 h-150 cursor-pointer"
                    :style="`overflow: hidden; background-image: url('${getPrevImage}'); background-size: cover; background-position: center; background-repeat: no-repeat;`"
                    @click="prev"
                >
                </Card>
            </div>

            <!-- Current Card (Center) -->
            <div class="opacity-100 z-10">
                <Card
                    class="w-96 h-170 cursor-pointer"
                    :style="`overflow: hidden; background-image: url('${getCurrentImage}'); background-size: cover; background-position: center; background-repeat: no-repeat;`"
                >
                </Card>
            </div>

            <!-- Next Card (Right) -->
            <div class="absolute right-3 lg:right-140 opacity-60">
                <Card
                    class="w-96 h-150 cursor-pointer"
                    :style="`overflow: hidden; background-image: url('${getNextImage}'); background-size: cover; background-position: center; background-repeat: no-repeat;`"
                    @click="next"
                >
                </Card>
            </div>
        </div>

        <!-- Action Buttons -->
        <div class="absolute bottom-30 lg:bottom-20 left-1/2 transform -translate-x-1/2 flex gap-4 z-20">
            <Button
                class="!w-20 !h-20 !text-4xl bg-white bg-opacity-90 !outline-none !ring-0 !border-0"
                icon="pi pi-times"
                raised
                rounded
                size="large"
                style="outline: none !important; box-shadow: none !important;"
                @click="handleClickAnimation()"
            >
                <i class="pi pi-times" style="color: red"></i>
            </Button>
            <Button
                class="!w-20 !h-20 !text-4xl bg-white bg-opacity-90 !outline-none !ring-0 !border-0"
                icon="pi pi-heart"
                raised
                rounded
                size="large"
                style="outline: none !important; box-shadow: none !important;"
                @click="handleHeartClick()"
            >
                <i class="pi pi-heart" style="color: green;"></i>
            </Button>
        </div>
    </div>
</template>

<style scoped>
</style>