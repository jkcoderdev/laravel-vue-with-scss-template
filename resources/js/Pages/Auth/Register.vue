<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Register" />

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="name" value="Name" />

                <TextInput
                    id="name"
                    type="text"
                    class="input"
                    v-model="form.name"
                    required
                    autofocus
                    autocomplete="name"
                />

                <InputError class="error" :message="form.errors.name" />
            </div>

            <div>
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="input"
                    v-model="form.email"
                    required
                    autocomplete="username"
                />

                <InputError class="error" :message="form.errors.email" />
            </div>

            <div>
                <InputLabel for="password" value="Password" />

                <TextInput
                    id="password"
                    type="password"
                    class="input"
                    v-model="form.password"
                    required
                    autocomplete="new-password"
                />

                <InputError class="error" :message="form.errors.password" />
            </div>

            <div>
                <InputLabel
                    for="password_confirmation"
                    value="Confirm Password"
                />

                <TextInput
                    id="password_confirmation"
                    type="password"
                    class="input"
                    v-model="form.password_confirmation"
                    required
                    autocomplete="new-password"
                />

                <InputError
                    class="error"
                    :message="form.errors.password_confirmation"
                />
            </div>

            <div>
                <Link
                    :href="route('login')"
                    class="link"
                >
                    Already registered?
                </Link>

                <PrimaryButton
                    class="submit-button"
                    :class="{ 'disabled': form.processing }"
                    :disabled="form.processing"
                >
                    Register
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>

<style lang="scss" scoped>
form {
    display: flex;
    flex-direction: column;
    gap: 1rem;

    .input {
        margin-top: 0.25rem;
        width: 100%;
        display: block;
    }

    .error {
        margin-top: 0.5rem;
    }

    & > div:last-child {
        display: flex;
        align-items: center;
        justify-content: flex-end;
    }
    
    .link {
        border-radius: 0.375rem;

        font-size: 0.875rem;
        line-height: 1.25rem;

        text-decoration: underline;

        color: #4b5563;

        &:hover {
            color: #111827;
        }

        &:focus {
            outline: 2px solid transparent;
            outline-offset: 2px;

            box-shadow: 0 0 0 2px #ffffff, 0 0 0 4px #6366f1;
        }
    }

    .submit-button {
        margin-inline-start: 1rem;

        &.disabled {
            opacity: 0.25;
        }
    }
}
</style>
