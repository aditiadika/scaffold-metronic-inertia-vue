<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto px-8">
                <div class="card overflow-hidden shadow-sm rounded-2">
                    <div class="p-6 text-gray-900">You're logged in! here</div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
