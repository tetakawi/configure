<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const slides = ref([
    {
        title: 'Empalme Manufacturing Campus',
        image: '/images/slide1.png',
    },
    {
        title: 'Zapa Manufacturing Campus',
        image: '/images/slide2.png',
    },
    {
        title: 'Guaymas Manufacturing Campus',
        image: '/images/slide3.png',
    },
    {
        title: 'Hermosillo Manufacturing Campus',
        image: '/images/slide4.png',
    },
    {
        title: 'Mazatlán Manufacturing Campus',
        image: '/images/slide5.png',
    },
])

const currentIndex = ref(0)
let interval = null

const nextSlide = () => {
    currentIndex.value = (currentIndex.value + 1) % slides.value.length
}

onMounted(() => {
    interval = setInterval(nextSlide, 5000) // cambia cada 5 segundos
})

onUnmounted(() => {
    clearInterval(interval)
})
</script>

<template>
    <div class="relative w-full h-full overflow-hidden">

        <!-- Imagen -->
        <div
            class="absolute inset-0 bg-cover bg-center transition-all duration-700"
            :style="{ backgroundImage: `url(${slides[currentIndex].image})` }"
        ></div>

        <!-- Overlay oscuro -->
        <div class="absolute inset-0 bg-black/30"></div>

        <!-- Texto y controles -->
        <div class="absolute bottom-8 left-8 text-white z-10">
            <h2 class="text-lg font-semibold mb-4">
                {{ slides[currentIndex].title }}
            </h2>

            <div class="flex items-center gap-2">
                <div
                    v-for="(slide, index) in slides"
                    :key="index"
                    class="h-2 rounded-full transition-all duration-300"
                    :class="index === currentIndex
                        ? 'w-10 bg-white'
                        : 'w-2 bg-white/50'"
                ></div>
            </div>
        </div>

    </div>
</template>