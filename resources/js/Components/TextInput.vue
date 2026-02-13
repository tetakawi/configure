<script setup>
import { onMounted, ref, computed } from 'vue';

const model = defineModel({
    type: String,
    required: true,
});

const props = defineProps({
    type: {
        type: String,
        default: 'text',
    },
});

const input = ref(null);
const showPassword = ref(false);

const inputType = computed(() => {
    if (props.type === 'password') {
        return showPassword.value ? 'text' : 'password';
    }
    return props.type;
});

onMounted(() => {
    if (input.value?.hasAttribute('autofocus')) {
        input.value.focus();
    }
});

defineExpose({ focus: () => input.value?.focus() });
</script>

<template>
    <div class="relative">
        <input
            :type="inputType"
            class="w-full rounded-md border-gray-300 shadow-sm pr-10 focus:border-[#0071ce] focus:ring-[#0071ce]"
            v-model="model"
            ref="input"
        />

        <!-- Icono solo si es password -->
        <button
            v-if="props.type === 'password'"
            type="button"
            @click="showPassword = !showPassword"
            class="absolute inset-y-0 right-0 flex items-center pr-3 text-gray-400 hover:text-gray-600"
        >
            <!-- Ojo cerrado -->
            <svg
                v-if="!showPassword"
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
            >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M15 12m-3 0a3 3 0 106 0a3 3 0 10-6 0M2.458 12C3.732 7.943 7.523 5 12 5
                    c4.477 0 8.268 2.943 9.542 7
                    -1.274 4.057-5.065 7-9.542 7
                    -4.477 0-8.268-2.943-9.542-7z" />
            </svg>

            <!-- Ojo abierto -->
            <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
            >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M13.875 18.825A10.05 10.05 0 0112 19
                    c-4.478 0-8.268-2.943-9.542-7
                    a9.956 9.956 0 012.293-3.95
                    M6.423 6.423A9.956 9.956 0 0112 5
                    c4.477 0 8.268 2.943 9.542 7
                    a9.966 9.966 0 01-4.043 5.18
                    M15 12a3 3 0 00-3-3
                    m0 0a3 3 0 00-3 3
                    m3-3l6 6m-6-6l-6 6" />
            </svg>
        </button>
    </div>
</template>