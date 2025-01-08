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

const maxWidthClass = computed(() => props.maxWidth);
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
                enter-active-class="transition-animation-enter-active"
                enter-from-class="transition-animation-enter-from"
                enter-to-class="transition-animation-enter-to"
                leave-active-class="transition-animation-leave-active"
                leave-from-class="transition-animation-leave-from"
                leave-to-class="transition-animation-leave-to"
            >
                <div
                    v-show="show"
                    class="animation"
                    @click="close"
                >
                    <div class="background"></div>
                </div>
            </Transition>

            <Transition
                enter-active-class="transition-modal-enter-active"
                enter-from-class="transition-modal-enter-from"
                enter-to-class="transition-modal-enter-to"
                leave-active-class="transition-modal-leave-active"
                leave-from-class="transition-modal-leave-from"
                leave-to-class="transition-modal-leave-to"
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
.dialog {
    margin: 0;

    min-height: 100%;
    min-width: 100%;

    z-index: 50;
    overflow-y: auto;

    background-color: transparent;

    &::backdrop {
        background-color: transparent;
    }

    .content {
        padding: 1.5rem 1rem;

        position: fixed;
        inset: 0;

        z-index: 50;
        overflow-y: auto;

        @media (min-width: 640px) {
            padding-left: 0;
            padding-right: 0;
        }

        .animation {
            position: fixed;
            inset: 0;

            transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);

            .background {
                position: absolute;
                inset: 0;

                background-color: #6b7280;
                opacity: 75%;
            }
        }

        .message {
            margin-bottom: 1.5rem;

            overflow: hidden;

            border: 0.5rem;
            background-color: #ffffff;

            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);

            transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);

            @media (min-width: 640px) {
                margin-left: auto;
                margin-right: auto;
                width: 100%;

                .sm {
                    max-width: 24rem;
                }

                .md {
                    max-width: 28rem;
                }

                .lg {
                    max-width: 32rem;
                }

                .xl {
                    max-width: 36rem;
                }

                .xxl {
                    max-width: 42rem;
                }
            }
        }
    }
}

// Animation transition classes

.transition-animation-enter-active {
    transition-timing-function: cubic-bezier(0, 0, 0.2, 1); // ease-out
    transition-duration: 0.3s;
}

.transition-animation-enter-from {
    opacity: 0;
}

.transition-animation-enter-to {
    opacity: 1;
}

.transition-animation-leave-active {
    transition-timing-function: cubic-bezier(0.4, 0, 1, 1); // ease-out
    transition-duration: 0.2s;
}

.transition-animation-leave-from {
    opacity: 1;
}

.transition-animation-leave-to {
    opacity: 0;
}

// Modal transition classes

.transition-modal-enter-active {
    transition-timing-function: cubic-bezier(0, 0, 0.2, 1); // ease-in
    transition-duration: 0.3s;
}

.transition-modal-enter-from {
    opacity: 0;
    translate: 0 1rem;

    @media (min-width: 640px) {
        translate: 0 0;
        scale: 95%;
    }
}

.transition-modal-enter-to {
    opacity: 1;
    translate: 0 0;

    @media (min-width: 640px) {
        scale: 100%;
    }
}

.transition-modal-leave-active {
    transition-timing-function: cubic-bezier(0.4, 0, 1, 1); // ease-out
    transition-duration: 0.2s;
}

.transition-modal-leave-from {
    opacity: 1;
    translate: 0 0;

    @media (min-width: 640px) {
        scale: 100%;
    }
}

.transition-modal-leave-to {
    opacity: 0;
    translate: 0 1rem;

    @media (min-width: 640px) {
        translate: 0 0;
        scale: 95%;
    }
}
</style>
