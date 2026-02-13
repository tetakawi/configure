<script setup>
import { onMounted, ref, computed } from 'vue';
import { EyeIcon, EyeSlashIcon } from '@heroicons/vue/24/outline';

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
            class="absolute inset-y-0 right-0 flex items-center pr-3 text-gray-400 hover:text-[#0071ce] transition-colors duration-200"
        >
            <EyeIcon
                v-if="!showPassword"
                class="h-4 w-4"
            />
            <EyeSlashIcon
                v-else
                class="h-4 w-4"
            />
        </button>
    </div>
</template>