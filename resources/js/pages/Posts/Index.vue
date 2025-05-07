<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, Link } from '@inertiajs/vue3';
import { Post } from '@/types/oox.d';
import { usePage } from '@inertiajs/vue3';
// import { LoaderCircle } from 'lucide-vue-next';

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Posts',
        href: '/posts',
    },
];

/* 3 formas de obtener props */
// define props - forma 1
/* const props = defineProps(
    {
        posts: Array,
    }
);  */
// define props - forma 1.1
defineProps({posts: Array});

// define props - forma 2
// const props = defineProps<{ posts: Post[] }>();

// get posts - forma 3
// const page = usePage<{ posts: Post[] }>();
// const posts = page.props.posts;

</script>

<template>
    <Head title="Posts" />
    
    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="flex h-full flex-1 flex-col gap-4 rounded-xl p-4">
        <!-- Create a Post Button -->
        <div>
            <Link
                :href="route('posts.create')"
                class="rounded-sm bg-green-700 px-3 py-2 text-xs font-medium text-white hover:bg-green-800 focus:ring-4 focus:ring-green-300 focus:outline-none dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800"
            >
                Create Post
            </Link>
        </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left text-sm text-zinc-500 rtl:text-right dark:text-zinc-400">
                    <thead class="bg-zinc-50 text-xs text-zinc-700 uppercase dark:bg-zinc-700 dark:text-zinc-400">
                        <tr>
                            <th scope="col" class="px-6 py-3">ID</th>
                            <th scope="col" class="px-6 py-3">Title</th>
                            <th scope="col" class="px-6 py-3">Body</th>
                            <th scope="col" class="px-6 py-3">Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                            v-for="post in posts"
                            :key="post.id"
                            class="border-b border-zinc-200 odd:bg-white even:bg-zinc-50 dark:border-zinc-700 odd:dark:bg-zinc-900 even:dark:bg-zinc-800"
                        >
                            <td class="px-6 py-2 font-medium text-zinc-900 dark:text-white">{{ post.id }}</td>
                            <td class="px-6 py-2 text-zinc-600 dark:text-zinc-300">{{ post.title }}</td>
                            <td class="px-6 py-2 text-zinc-600 dark:text-zinc-300">{{ post.body }}</td>
                            <td class="px-6 py-2">
                                <Link :href="route('posts.edit', post.id)" class=" rounded-lg bg-blue-700 px-3 py-2 text-xs font-medium text-white hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 focus:outline-none dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Edit</Link>
                                <button
                                    class="ml-1 cursor-pointer rounded-lg bg-red-700 px-3 py-2 text-xs font-medium text-white hover:bg-red-800 focus:ring-4 focus:ring-red-300 focus:outline-none dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800"
                                >
                                    <Link :href="route('posts.destroy', post.id)" method="delete" as="button" :preserve-scroll="true">
                                        <!-- <LoaderCircle v-if="form.processing" class="h-4 w-4 animate-spin" /> -->
                                        Delete
                                    </Link>
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </AppLayout>
</template>
