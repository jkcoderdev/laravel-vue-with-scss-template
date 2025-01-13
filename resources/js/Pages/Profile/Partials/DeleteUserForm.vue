<script setup>
import DangerButton from '@/Components/DangerButton.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import Modal from '@/Components/Modal.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useForm } from '@inertiajs/vue3';
import { nextTick, ref } from 'vue';

const confirmingUserDeletion = ref(false);
const passwordInput = ref(null);

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    confirmingUserDeletion.value = true;

    nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onError: () => passwordInput.value.focus(),
        onFinish: () => form.reset(),
    });
};

const closeModal = () => {
    confirmingUserDeletion.value = false;

    form.clearErrors();
    form.reset();
};
</script>

<template>
    <section>
        <header>
            <h2>
                Delete Account
            </h2>

            <p class="description">
                Once your account is deleted, all of its resources and data will
                be permanently deleted. Before deleting your account, please
                download any data or information that you wish to retain.
            </p>
        </header>

        <DangerButton @click="confirmUserDeletion" class="btn">Delete Account</DangerButton>

        <Modal :show="confirmingUserDeletion" @close="closeModal">
            <div class="modal">
                <h2>
                    Are you sure you want to delete your account?
                </h2>

                <p class="description">
                    Once your account is deleted, all of its resources and data
                    will be permanently deleted. Please enter your password to
                    confirm you would like to permanently delete your account.
                </p>

                <div class="input">
                    <InputLabel
                        for="password"
                        value="Password"
                        class="label"
                    />

                    <TextInput
                        id="password"
                        ref="passwordInput"
                        v-model="form.password"
                        type="password"
                        class="text-input"
                        placeholder="Password"
                        @keyup.enter="deleteUser"
                    />

                    <InputError :message="form.errors.password" class="input-error" />
                </div>

                <div class="btns">
                    <SecondaryButton @click="closeModal">
                        Cancel
                    </SecondaryButton>

                    <DangerButton
                        class="danger-btn"
                        :class="{ 'opaque': form.processing }"
                        :disabled="form.processing"
                        @click="deleteUser"
                    >
                        Delete Account
                    </DangerButton>
                </div>
            </div>
        </Modal>
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

    .description{
        @include smalltext;  

        margin-top: .25rem;
        color: $ligt-gray;
    }
}

.btn{
    margin-top: 1.5rem;
}

section{
    padding: 1.5rem;
    max-width: min-content;
    

    h2{
        @include largetext;
        font-weight: 500;
        color: $semi-black;
    }

    .modal{

        padding: 1.5rem;

        .input{
            margin-top: 1.5rem;

            .label{
                position: absolute;
                width: 1px;
                height: 1px;
                padding: 0;
                margin: -1px;
                overflow: hidden;
                clip: rect(0, 0, 0, 0);
                white-space: nowrap;
                border-width: 0;
            }

            .text-input{
                margin-top: .25rem;
                display: block;
                width: 75%;
            }
    
            .input-error{
                margin-top: .5rem;
            }
        }

        

        .btns{
            display: flex;
            align-items: center;
            margin-top: 1.5rem;

            .danger-btn{
                margin-inline-start: .75rem;

                .opaque{
                    opacity: 25% ;
                }
            }
        }

    }
    
}
</style>
