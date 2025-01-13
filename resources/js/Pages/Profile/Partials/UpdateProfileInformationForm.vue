<script setup>
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Link, useForm, usePage } from '@inertiajs/vue3';

defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const user = usePage().props.auth.user;

const form = useForm({
    name: user.name,
    email: user.email,
});
</script>

<template>
    <section>
        <header class="text-box">
            <h2>
                Profile Information
            </h2>

            <p>
                Update your account's profile information and email address.
            </p>
        </header>

        <form
            @submit.prevent="form.patch(route('profile.update'))"
            class="form"
        >
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

            <div v-if="mustVerifyEmail && user.email_verified_at === null">
                <p class="email">
                    Your email address is unverified.
                    <Link
                        :href="route('verification.send')"
                        method="post"
                        as="button"
                        class="link"
                    >
                        Click here to re-send the verification email.
                    </Link>
                </p>

                <div
                    v-show="status === 'verification-link-sent'"
                    class="message"
                >
                    A new verification link has been sent to your email address.
                </div>
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

            .email {
                margin-top: 0.5rem;

                font-size: 0.875rem;
                line-height: 1.25rem;

                color: #1f2937;

                .link {
                    font-size: 0.875rem;
                    line-height: 1.25rem;

                    border-radius: 0.375rem;
                    color: #4b5563;
                    text-decoration: underline;

                    &:hover {
                        color: #111827;
                    }

                    &:focus {
                        box-shadow: 0 0 0 2px #ffffff, 0 0 0 4px #6366f1;
                    }
                }
            }

            .message {
                margin-top: 0.5rem;
                font-size: 0.875rem;
                line-height: 1.25rem;
                color: #16a34a;
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
// $semi-black: #111;
// $gray: #333;
// $ligt-gray: #666;
// $indigo: #6366f1;

// @mixin smalltext{
//     font-size: 0.875rem;
//     line-height: 1.25rem;
// }

// @mixin largetext{
//     line-height: 1.75rem;
//     font-weight: 500;
// }

// header{
//     h2{
//         @include largetext;

//         font-size: 1.125rem;
//         color: $gray;
//     }

//     .desc{
//         @include smalltext;  

//         margin-top: .25rem;
//         color: $ligt-gray;
//     }
// }

// form{
//     margin-top: 1.5rem;
//     margin-bottom: 1.5rem;

//     .text-input{
//         margin-top: .25rem;
//         display: block;
//         width: 100%;
//     }

//     .input-error{
//         margin-top: .5rem;
//     }

//     .verify-email{
//         @include smalltext;

//         margin-top: .5rem;
//         color: $gray;

//         .link{
//             border-radius: 0.375rem;
//             @include smalltext;
//             color: $ligt-gray;
//             text-decoration: underline;
            
//             &:hover{
//                 color: $semi-black;
//             }

//             &:focus{
//                 outline: none;
//                 box-shadow: 0 0 0 2px $indigo, 0 0 0 4px rgba(255, 255, 255, 1);
//             }
//         }

//         .message{
//             @include smalltext;

//             margin-top: .5rem;
//             font-weight: 500;
//             color: rgb(0, 156, 0);
//         }
        
//     }

//     .btn{
//         display: flex;
//         align-items: center;
//         gap: 1rem;
//         margin-top: 1rem;

//         .message{
//             @include smalltext;

//             color: $ligt-gray;
//         }
//     }

    
// }
</style>
