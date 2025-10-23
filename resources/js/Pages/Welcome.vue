<script setup>
import { Head, Link } from "@inertiajs/vue3";
import { Check, Shield, Users, Zap } from "lucide-vue-next";

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
});
</script>

<template>
    <Head title="Welcome" />

    <div
        class="min-h-screen bg-gradient-to-br from-indigo-50 via-white to-purple-50"
    >
        <!-- Navigation -->
        <nav
            class="bg-white/80 backdrop-blur-sm border-b border-gray-200 sticky top-0 z-50"
        >
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center h-16">
                    <div class="flex items-center gap-2">
                        <div
                            class="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center"
                        >
                            <Check class="w-5 h-5 text-white" />
                        </div>
                        <span class="text-xl font-bold text-gray-900"
                            >TodoApp</span
                        >
                    </div>

                    <div v-if="canLogin" class="flex gap-4">
                        <Link
                            :href="route('login')"
                            class="px-4 py-2 text-gray-700 hover:text-gray-900 font-medium"
                        >
                            Log in
                        </Link>
                        <Link
                            v-if="canRegister"
                            :href="route('register')"
                            class="px-6 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 font-medium transition-colors"
                        >
                            Get Started
                        </Link>
                    </div>
                </div>
            </div>
        </nav>

        <!-- Hero Section -->
        <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-20 pb-24">
            <div class="text-center">
                <div
                    class="inline-flex items-center gap-2 px-4 py-2 bg-indigo-100 text-indigo-700 rounded-full text-sm font-medium mb-6"
                >
                    <Zap class="w-4 h-4" />
                    Simple. Fast. Powerful.
                </div>

                <h1
                    class="text-5xl md:text-6xl font-bold text-gray-900 mb-6 leading-tight"
                >
                    Organize Your Life,
                    <br />
                    <span
                        class="bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent"
                    >
                        One Task at a Time
                    </span>
                </h1>

                <p class="text-xl text-gray-600 mb-10 max-w-2xl mx-auto">
                    The simplest way to manage your todos. Stay organized, boost
                    productivity, and never forget a task again.
                </p>

                <p class="text-sm text-gray-500 mt-4">
                    No credit card required • Free forever
                </p>
            </div>

            <!-- Demo Preview -->
            <div class="mt-16 relative">
                <div
                    class="bg-white rounded-2xl shadow-2xl border border-gray-200 p-8 max-w-4xl mx-auto"
                >
                    <div class="space-y-3">
                        <!-- Todo Items Preview -->
                        <div
                            v-for="(todo, i) in [
                                {
                                    text: 'Build an amazing product',
                                    completed: true,
                                },
                                {
                                    text: 'Launch to the world',
                                    completed: false,
                                },
                                { text: 'Celebrate success', completed: false },
                            ]"
                            :key="i"
                            class="flex items-center gap-3 p-4 bg-gray-50 rounded-lg"
                        >
                            <div
                                :class="[
                                    'w-5 h-5 rounded border-2 flex items-center justify-center',
                                    todo.completed
                                        ? 'bg-indigo-600 border-indigo-600'
                                        : 'border-gray-300',
                                ]"
                            >
                                <Check
                                    v-if="todo.completed"
                                    class="w-3 h-3 text-white"
                                />
                            </div>
                            <span
                                :class="[
                                    'flex-1',
                                    todo.completed
                                        ? 'line-through text-gray-400'
                                        : 'text-gray-700',
                                ]"
                            >
                                {{ todo.text }}
                            </span>
                        </div>

                        <!-- Add todo preview -->
                        <div
                            class="flex items-center gap-2 p-4 bg-gray-50 rounded-lg border-2 border-dashed border-gray-300"
                        >
                            <input
                                type="text"
                                placeholder="Add a new task..."
                                class="flex-1 bg-transparent border-none outline-none text-gray-500 focus:ring-0"
                                disabled
                            />
                            <button
                                class="px-4 py-2 bg-indigo-600 text-white rounded-lg text-sm font-medium"
                            >
                                Add
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Features -->
        <section class="bg-white py-24">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center mb-16">
                    <h2
                        class="text-3xl md:text-4xl font-bold text-gray-900 mb-4"
                    >
                        Everything you need to stay productive
                    </h2>
                    <p class="text-lg text-gray-600 max-w-2xl mx-auto">
                        Powerful features that help you manage tasks
                        effortlessly
                    </p>
                </div>

                <div class="grid md:grid-cols-3 gap-8">
                    <div
                        class="p-8 rounded-2xl bg-gradient-to-br from-indigo-50 to-white border border-indigo-100"
                    >
                        <div
                            class="w-12 h-12 bg-indigo-600 rounded-xl flex items-center justify-center mb-4"
                        >
                            <Zap class="w-6 h-6 text-white" />
                        </div>
                        <h3 class="text-xl font-bold text-gray-900 mb-2">
                            Lightning Fast
                        </h3>
                        <p class="text-gray-600">
                            Add, edit, and complete tasks in milliseconds. No
                            lag, no waiting.
                        </p>
                    </div>

                    <div
                        class="p-8 rounded-2xl bg-gradient-to-br from-purple-50 to-white border border-purple-100"
                    >
                        <div
                            class="w-12 h-12 bg-purple-600 rounded-xl flex items-center justify-center mb-4"
                        >
                            <Shield class="w-6 h-6 text-white" />
                        </div>
                        <h3 class="text-xl font-bold text-gray-900 mb-2">
                            Secure & Private
                        </h3>
                        <p class="text-gray-600">
                            Your tasks are encrypted and private. Only you can
                            see your todos.
                        </p>
                    </div>

                    <div
                        class="p-8 rounded-2xl bg-gradient-to-br from-pink-50 to-white border border-pink-100"
                    >
                        <div
                            class="w-12 h-12 bg-pink-600 rounded-xl flex items-center justify-center mb-4"
                        >
                            <Users class="w-6 h-6 text-white" />
                        </div>
                        <h3 class="text-xl font-bold text-gray-900 mb-2">
                            Personal Dashboard
                        </h3>
                        <p class="text-gray-600">
                            Your own space to organize tasks exactly how you
                            want them.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- CTA -->
        <section class="py-24">
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
                <div
                    class="bg-gradient-to-r from-indigo-600 to-purple-600 rounded-3xl p-12 text-center text-white relative overflow-hidden"
                >
                    <div class="relative">
                        <h2 class="text-3xl md:text-4xl font-bold mb-4">
                            Ready to get organized?
                        </h2>
                        <p
                            class="text-lg text-indigo-100 mb-8 max-w-2xl mx-auto"
                        >
                            Join thousands of productive people managing their
                            tasks with TodoApp
                        </p>
                        <Link
                            :href="route('register')"
                            class="inline-block px-8 py-4 bg-white text-indigo-600 rounded-lg hover:bg-gray-50 font-semibold text-lg transition-colors shadow-xl"
                        >
                            Get Started Now
                        </Link>
                    </div>
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="bg-gray-900 text-white py-12">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center">
                    <div class="flex items-center gap-2">
                        <div
                            class="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center"
                        >
                            <Check class="w-5 h-5 text-white" />
                        </div>
                        <span class="text-xl font-bold">TodoApp</span>
                    </div>
                    <div class="text-gray-400 text-sm">
                        © 2024 TodoApp. Built with Laravel & Vue.js
                    </div>
                </div>
            </div>
        </footer>
    </div>
</template>
