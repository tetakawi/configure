<script setup>
import { Link } from '@inertiajs/vue3';
import LoginSlider from '@/Components/LoginSlider.vue';
</script>

<template>
    <div class="flex min-h-screen">

        <!-- LEFT PANEL -->
        <div class="flex w-full lg:w-1/3 items-center justify-center bg-white px-10">
            <div class="w-full max-w-sm">

                <!-- Logo -->
                <div class="mb-10 text-center">
                    <img
                        src="/images/tetakawi-logo.png"
                        alt="Tetakawi"
                        class="mx-auto h-10"
                    />
                    <h2 class="mt-4 text-lg font-semibold text-gray-700">
                        Mexico Business Case Portal
                    </h2>
                </div>

                <!-- Slot (Login Form) -->
                <slot />

                <!-- Footer -->
                <div class="mt-16 text-xs text-gray-400 text-center">
                    © 2026 Tetakawi. All rights reserved.
                </div>

            </div>
        </div>

        <!-- RIGHT PANEL (IMAGE) -->
       <div class="hidden lg:block lg:w-2/3 h-screen">
            <LoginSlider />
        </div>

    </div>
</template>
