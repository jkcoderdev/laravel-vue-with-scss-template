<script setup>
import { computed, onMounted, onUnmounted, ref, watch } from 'vue';

const props = defineProps({
    show: {
        type: Boolean,
        default: false,
    },
    maxWidth: {
        type: String,
        default: 'xxl',
    },
    closeable: {
        type: Boolean,
        default: true,
    },
});

const emit = defineEmits(['close']);
const dialog = ref();
const showSlot = ref(props.show);

watch(
    () => props.show,
    () => {
        if (props.show) {
            document.body.style.overflow = 'hidden';
            showSlot.value = true;

            dialog.value?.showModal();
        } else {
            document.body.style.overflow = '';

            setTimeout(() => {
                dialog.value?.close();
                showSlot.value = false;
            }, 200);
        }
    },
);

const close = () => {
    if (props.closeable) {
        emit('close');
    }
};

const closeOnEscape = (e) => {
    if (e.key === 'Escape') {
        e.preventDefault();

        if (props.show) {
            close();
        }
    }
};

onMounted(() => document.addEventListener('keydown', closeOnEscape));

onUnmounted(() => {
    document.removeEventListener('keydown', closeOnEscape);

    document.body.style.overflow = '';
});

const maxWidthClass = computed(() => {
    return {
        sm: 'sm',
        md: 'md',
        lg: 'lg',
        xl: 'xl',
        'xxl': '2xl',
    }[props.maxWidth];
});
</script>

<template>
    <dialog
        class="dialog"
        ref="dialog"
    >
        <div
            class="content"
            scroll-region
        >
            <Transition
                enter-active-class="ease-out duration-300"
                enter-from-class="opacity-0"
                enter-to-class="opacity-100"
                leave-active-class="ease-in duration-200"
                leave-from-class="opacity-100"
                leave-to-class="opacity-0"
            >
                <div
                    v-show="show"
                    class="fixed inset-0 transform transition-all animation"
                    @click="close"
                >
                    <div
                        class="absolute inset-0 bg-gray-500 opacity-75"
                    />
                </div>
            </Transition>

            <Transition
                enter-active-class="ease-out duration-300"
                enter-from-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                enter-to-class="opacity-100 translate-y-0 sm:scale-100"
                leave-active-class="ease-in duration-200"
                leave-from-class="opacity-100 translate-y-0 sm:scale-100"
                leave-to-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            >
                <div
                    v-show="show"
                    class="message"
                    :class="maxWidthClass"
                >
                    <slot v-if="showSlot" />
                </div>
            </Transition>
        </div>
    </dialog>
</template>

<style lang="scss" scoped>
    .dialog{
        margin: 0;
        min-height: 100%;
        min-width: 100%;

        z-index: 50;
        overflow-y: auto;

        background-color: transparent;
        &::backdrop{
            background-color: transparent;
        }

        .content{
            position: fixed;

            inset: 0;
            z-index: 50;
            overflow-y: auto;
            padding: 1.5rem 1rem;

            @media (min-width: 640px) {
                padding-left: 0;
                padding-right: 0;
            }

            .message{
                margin-bottom: 1.5rem;
                overflow: hidden;

                border: 0.5rem;
                background-color: white;

                transition: all 150ms cubic-bezier(0.4, 0, 0.2, 1);

                @media (min-width: 640px) {
                    margin-left: auto;
                    margin-right: auto;
                    width: 100%;
                }

                // These one are very tailwind heavy...

                transform: translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y));

                --tw-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
                --tw-shadow-colored: 0 20px 25px -5px var(--tw-shadow-color), 0 8px 10px -6px var(--tw-shadow-color);
                box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow);
            }

        }
    }

    @media (min-width: 640px) {

        .sm {
            max-width: 24rem;
        }

        .md{
            max-width: 28rem;
        }
    
        .lg{
            max-width: 32rem;
        }
    
        .xl{
            max-width: 36rem;
        }
    
        .xxl{
            max-width: 42rem;
        }

    }

    
</style>
