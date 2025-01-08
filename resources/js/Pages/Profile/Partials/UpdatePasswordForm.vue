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
        <header>
            <h2 >
                Update Password
            </h2>

            <p class="desc">
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
                    class="text-input"
                    autocomplete="current-password"
                />

                <InputError
                    :message="form.errors.current_password"
                    class="input-error"
                />
            </div>

            <div>
                <InputLabel for="password" value="New Password" />

                <TextInput
                    id="password"
                    ref="passwordInput"
                    v-model="form.password"
                    type="password"
                    class="text-input"
                    autocomplete="new-password"
                />

                <InputError :message="form.errors.password" class="input-error" />
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
                    class="text-input"
                    autocomplete="new-password"
                />

                <InputError
                    :message="form.errors.password_confirmation"
                    class="input-error"
                />
            </div>

            <div class="btn">
                <PrimaryButton :disabled="form.processing">Save</PrimaryButton>

                <Transition
                    enter-active-class="transition ease-in-out"
                    enter-from-class="opacity-0"
                    leave-active-class="transition ease-in-out"
                    leave-to-class="opacity-0"
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
    $semi-black: #111;
    $gray: #333;
    $ligt-gray: #666;
    $indigo: #6366f1;

    @mixin smalltext{
        font-size: 0.875rem;
        line-height: 1.25rem;
    }

    @mixin largetext{
        line-height: 1.75rem;
        font-weight: 500;
    }

    header{
        h2{
            @include largetext;

            font-size: 1.125rem;
            color: $gray;
        }

        .desc{
            @include smalltext;  

            margin-top: .25rem;
            color: $ligt-gray;
        }
    }

    form{
        margin-top: 1.5rem;
        margin-bottom: 1.5rem;

        .text-input{
            margin-top: .25rem;
            display: block;
            width: 100%;
        }

        .input-error{
            margin-top: .5rem;
        }

        .btn{
            display: flex;
            align-items: center;
            gap: 1rem;
            margin-top: 1rem;

            .message{
                @include smalltext;

                color: $ligt-gray;
            }
        }
    }


</style>
