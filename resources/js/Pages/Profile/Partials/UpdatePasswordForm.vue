<script setup>
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

const updatePassword = () => {
    form.put(route('password.update'), {
        preserveScroll: true,
        onSuccess: () => form.reset(),
        onError: () => {
            if (form.errors.password) {
                form.reset('password', 'password_confirmation');
                passwordInput.value.focus();
            }
            if (form.errors.current_password) {
                form.reset('current_password');
                currentPasswordInput.value.focus();
            }
        },
    });
};
</script>

<template>
    <section>
        <header class="text-box">
            <h2>
                Update Password
            </h2>

            <p>
                Ensure your account is using a long, random password to stay
                secure.
            </p>
        </header>

        <form @submit.prevent="updatePassword" class="form">
            <div>
                <InputLabel for="current_password" value="Current Password" />

                <TextInput
                    id="current_password"
                    ref="currentPasswordInput"
                    v-model="form.current_password"
                    type="password"
                    class="input"
                    autocomplete="current-password"
                />

                <InputError
                    :message="form.errors.current_password"
                    class="error"
                />
            </div>

            <div>
                <InputLabel for="password" value="New Password" />

                <TextInput
                    id="password"
                    ref="passwordInput"
                    v-model="form.password"
                    type="password"
                    class="input"
                    autocomplete="new-password"
                />

                <InputError :message="form.errors.password" class="error" />
            </div>

            <div>
                <InputLabel
                    for="password_confirmation"
                    value="Confirm Password"
                />

                <TextInput
                    id="password_confirmation"
                    v-model="form.password_confirmation"
                    type="password"
                    class="input"
                    autocomplete="new-password"
                />

                <InputError
                    :message="form.errors.password_confirmation"
                    class="error"
                />
            </div>

            <div class="submit-box">
                <PrimaryButton :disabled="form.processing">Save</PrimaryButton>

                <Transition
                    enter-active-class="transition-enter-active"
                    enter-from-class="transition-enter-from"
                    leave-active-class="transition-leave-active"
                    leave-to-class="transition-leave-to"
                >
                    <p
                        v-if="form.recentlySuccessful"
                        class="message"
                    >
                        Saved.
                    </p>
                </Transition>
            </div>
        </form>
    </section>
</template>

<style lang="scss" scoped>
section {
    .text-box {
        h2 {
            font-size: 1.125rem;
            line-height: 1.75rem;
            font-weight: 500;
            color: #111827;
        }

        p {
            margin-top: 0.25rem;
            font-size: 0.875rem;
            line-height: 1.25rem;
            color: #4b5563;
        }
    }

    .form {
        margin-top: 1.5rem;

        display: flex;
        flex-direction: column;
        gap: 1.5rem;

        .input {
            margin-top: 0.25rem;
            width: 100%;
            display: block;
        }

        .error {
            margin-top: 0.5rem;
        }

        .submit-box {
            display: flex;
            align-items: center;
            gap: 1rem;

            .message {
                font-size: 0.875rem;
                line-height: 1.25rem;
                color: #4b5563;
            }

            .transition-enter-active,
            .transition-leave-active {
                transition-property: color;
                transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
                transition-duration: 0.15s;
            }

            .transition-enter-from,
            .transition-leave-to {
                opacity: 0;
            }
        }
    }
}
</style>
