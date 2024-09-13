<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';
import { Head } from '@inertiajs/vue3';
import Toolbar from '@/Layouts/Partials/Toolbar.vue';

defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
    title: {
        type: String,
    },
    breadcrumbs: {
        type: Object,
    }
});
</script>

<template>

    <Head title="Profile" />

    <AuthenticatedLayout>
        <template #header>
            <h2>Profile</h2>
        </template>

        <!--begin::Toolbar-->
        <Toolbar :title="title" :breadcrumbs="breadcrumbs"></Toolbar>
        <!--end::Toolbar-->

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">
                <div class="p-4 card rounded-3">
                    <UpdateProfileInformationForm :must-verify-email="mustVerifyEmail" :status="status"
                        class="max-w-xl" />
                </div>

                <div class="p-4 my-5 card rounded-3">
                    <UpdatePasswordForm class="max-w-xl" />
                </div>

                <div class="p-4 card rounded-3">
                    <DeleteUserForm class="max-w-xl" />
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
