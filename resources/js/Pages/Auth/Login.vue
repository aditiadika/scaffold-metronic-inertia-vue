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

        <div v-if="status" class="w-lg-500px bg-body rounded shadow-sm p-10 p-lg-15 mx-auto">
            {{ status }}
        </div>

        <div class="w-lg-500px bg-body rounded shadow-sm p-10 p-lg-15 mx-auto">
            <form @submit.prevent="submit" class="form w-100" novalidate="novalidate" id="kt_sign_in_form">
                <div class="text-center mb-10">
                    <!--begin::Title-->
                    <h1 class="text-dark mb-3">Sign In to Metronic</h1>
                    <!--end::Title-->
                    <!--begin::Link-->
                    <div class="text-gray-400 fw-bold fs-4">New Here?
                        <Link href="/register" class="link-primary fw-bolder">Create an Account</Link>
                    </div>
                    <!--end::Link-->
                </div>

                <div class="fv-row mb-10">
                    <InputLabel for="email" value="Email" />

                    <TextInput id="email" type="email" v-model="form.email" required autofocus
                        autocomplete="username" />

                    <InputError class="mt-2" :message="form.errors.email" />
                </div>

                <div class="fv-row mb-10">
                    <div class="d-flex flex-stack mb-2">
                        <InputLabel for="password" value="Password" />

                        <Link v-if="canResetPassword" :href="route('password.request')"
                            class="link-primary fs-6 fw-bolder">
                        Forgot your password?
                        </Link>
                    </div>

                    <TextInput id="password" type="password" v-model="form.password" required
                        autocomplete="current-password" />
                    <InputError class="mt-2" :message="form.errors.password" />
                </div>

                <div class="text-center">
                    <PrimaryButton class="btn-primary" :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing">
                        <span v-if="!form.processing" class="indicator-label">
                            Log in
                        </span>
                        <span v-else>
                            Please wait... <span class="spinner-border spinner-border-sm align-middle ms-2"></span>
                        </span>
                    </PrimaryButton>
                    <!--begin::Separator-->
                    <div class="text-center text-muted text-uppercase fw-bolder mb-5">or</div>
                    <!--end::Separator-->
                    <!--begin::Google link-->
                    <a href="#" class="btn btn-flex flex-center btn-light btn-lg w-100 mb-5">
                        <img alt="Logo" src="assets/media/svg/brand-logos/google-icon.svg"
                            class="h-20px me-3" />Continue with Google</a>
                    <!--end::Google link-->
                    <!--begin::Google link-->
                    <a href="#" class="btn btn-flex flex-center btn-light btn-lg w-100 mb-5">
                        <img alt="Logo" src="assets/media/svg/brand-logos/facebook-4.svg" class="h-20px me-3" />Continue
                        with Facebook</a>
                    <!--end::Google link-->
                    <!--begin::Google link-->
                    <a href="#" class="btn btn-flex flex-center btn-light btn-lg w-100">
                        <img alt="Logo" src="assets/media/svg/brand-logos/apple-black.svg"
                            class="h-20px me-3" />Continue with Apple</a>
                    <!--end::Google link-->
                </div>
            </form>
        </div>

    </GuestLayout>
</template>
