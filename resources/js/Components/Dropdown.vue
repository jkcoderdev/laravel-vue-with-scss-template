<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue';

const props = defineProps({
    align: {
        type: String,
        default: 'right',
    },
});

const closeOnEscape = (e) => {
    if (open.value && e.key === 'Escape') {
        open.value = false;
    }
};

onMounted(() => document.addEventListener('keydown', closeOnEscape));
onUnmounted(() => document.removeEventListener('keydown', closeOnEscape));

const alignmentClass = computed(() => {
    if (props.align === 'left') return 'align-left';
    if (props.align === 'right') return 'align-right';

    return '';
});

const open = ref(false);
</script>

<template>
    <div class="dropdown-container">
        <div @click="open = !open">
            <slot name="trigger" />
        </div>

        <!-- Full Screen Dropdown Overlay -->
        <div
            v-show="open"
            class="dropdown-overlay"
            @click="open = false"
        ></div>

        <Transition
            enter-active-class="transition-enter-active"
            enter-from-class="transition-enter-from"
            enter-to-class="transition-enter-to"
            leave-active-class="transition-leave-active"
            leave-from-class="transition-leave-from"
            leave-to-class="transition-leave-to"
        >
            <div
                v-show="open"
                class="dropdown-content"
                :class="alignmentClass"
                style="display: none"
                @click="open = false"
            >
                <div>
                    <slot name="content" />
                </div>
            </div>
        </Transition>
    </div>
</template>

<style lang="scss" scoped>
.dropdown-container {
    position: relative;
}

.dropdown-overlay {
    position: fixed;
    inset: 0;
    z-index: 40;
}

.dropdown-content {
    position: absolute;
    top: 100%;
    z-index: 50;

    width: 12rem;

    margin-top: 0.5rem;

    border-radius: 0.375rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -4px rgba(0, 0, 0, 0.1);

    transform-origin: top;

    &.align-left {
        inset-inline-start: 0;

        &:where([dir="ltr"], [dir="ltr"] *) {
            transform-origin: top left;
        }

        &:where([dir="rtl"], [dir="rtl"] *) {
            transform-origin: top right;
        }
    }

    &.align-right {
        inset-inline-end: 0;

        &:where([dir="ltr"], [dir="ltr"] *) {
            transform-origin: top right;
        }

        &:where([dir="rtl"], [dir="rtl"] *) {
            transform-origin: top left;
        }
    }

    & > div {
        border-radius: 0.375rem;
        box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.05);

        padding: 0.25rem 0;

        background-color: #ffffff;
    }
}

// Transition
.transition-enter-active {
    transition: 0.2s ease-out;
}

.transition-enter-from {
    opacity: 0;
    transform: scale(95%);
}

.transition-enter-to {
    opacity: 1;
    transform: scale(100%);
}

.transition-leave-active {
    transition: 0.075s ease-in;
}

.transition-leave-from {
    opacity: 1;
    transform: scale(100%);
}

.transition-leave-to {
    opacity: 0;
    transform: scale(95%);
}
</style>
