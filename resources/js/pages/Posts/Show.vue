<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, Link } from '@inertiajs/vue3';

// define props
const props = defineProps({
    post: Object,
});

// Breadcrumbs
const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Post Show',
        href: '/posts/show',
    },
];
</script>

<template>
    <Head title="Post Show" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-4 rounded-xl p-4">
            <!-- Go Back Button -->
            <div>
                <Link
                    :href="route('posts.index')"
                    class="rounded-sm bg-gray-700 px-3 py-2 text-xs font-medium text-white hover:bg-gray-800 focus:ring-4 focus:ring-gray-300 focus:outline-none dark:bg-gray-600 dark:hover:bg-gray-700 dark:focus:ring-gray-800"
                >
                    Go Back
                </Link>
            </div>
            <div class="overflow-x-auto">
                <div class="mx-auto mt-8 max-w-2xl space-y-4 rounded-xl border p-4 text-wrap">
                    <h1 class="text-2xl font-bold">{{ post.title }}</h1>
                    <p class="text-white/60 truncate"><pre>{{ post.body }}</pre></p>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
