<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <div v-if="status" class="status">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="input"
                    v-model="form.email"
                    required
                    autofocus
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
                    autocomplete="current-password"
                />

                <InputError class="error" :message="form.errors.password" />
            </div>

            <div>
                <label class="checkbox">
                    <Checkbox name="remember" v-model:checked="form.remember" />
                    <span class="checkbox-text"
                        >Remember me</span
                    >
                </label>
            </div>

            <div>
                <Link
                    v-if="canResetPassword"
                    :href="route('password.request')"
                    class="link"
                >
                    Forgot your password?
                </Link>

                <PrimaryButton
                    class="submit-button"
                    :class="{ 'disabled': form.processing }"
                    :disabled="form.processing"
                >
                    Log in
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>

<style lang="scss" scoped>
.status {
    margin-bottom: 1rem;

    font-size: 0.875rem;
    line-height: 1.25rem;

    font-weight: 500;

    color: #16a34a;
}

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

    .checkbox {
        display: flex;
        align-items: center;

        cursor: pointer;
        
        .checkbox-text {
            margin-inline-start: 0.5rem;

            font-size: 0.875rem;
            line-height: 1.25rem;

            color: #4b5563;

            -webkit-user-select: none;
            user-select: none;
        }
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
