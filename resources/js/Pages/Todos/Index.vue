<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head, useForm } from "@inertiajs/vue3";
import { ref } from "vue";

const props = defineProps({
    todos: Array,
});

// Form for creating new todo
const form = useForm({
    title: "",
});

// State for editing
const editingId = ref(null);
const editForm = useForm({
    title: "",
});

const submit = () => {
    form.post(route("todos.store"), {
        preserveScroll: true,
        onSuccess: () => {
            form.reset();
        },
    });
};

const toggleComplete = (todo) => {
    useForm({
        completed: !todo.completed,
    }).put(route("todos.update", todo.id), {
        preserveScroll: true,
    });
};

const startEdit = (todo) => {
    editingId.value = todo.id;
    editForm.title = todo.title;
};

const cancelEdit = () => {
    editingId.value = null;
    editForm.reset();
};

const updateTodo = (todo) => {
    editForm.put(route("todos.update", todo.id), {
        preserveScroll: true,
        onSuccess: () => {
            editingId.value = null;
            editForm.reset();
        },
    });
};

const deleteTodo = (todoId) => {
    if (confirm("Are you sure you want to delete this todo?")) {
        useForm({}).delete(route("todos.destroy", todoId), {
            preserveScroll: true,
        });
    }
};
</script>

<template>
    <Head title="Todos" />

    <AuthenticatedLayout>
        <template #header>
            <h2
                class="text-xl font-semibold leading-tight text-gray-800 dark:text-gray-200"
            >
                My Todos
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-3xl sm:px-6 lg:px-8">
                <div
                    class="overflow-hidden bg-white shadow-sm sm:rounded-lg dark:bg-gray-800"
                >
                    <div class="p-6 text-gray-900 dark:text-gray-100">
                        <!-- Create Todo Form -->
                        <form @submit.prevent="submit" class="mb-6">
                            <div class="flex gap-2">
                                <input
                                    v-model="form.title"
                                    type="text"
                                    placeholder="What needs to be done?"
                                    class="flex-1 rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-900 dark:text-gray-300"
                                    required
                                />
                                <button
                                    type="submit"
                                    :disabled="form.processing"
                                    class="rounded-md bg-indigo-600 px-4 py-2 text-white hover:bg-indigo-700 disabled:opacity-50"
                                >
                                    Add
                                </button>
                            </div>
                            <div
                                v-if="form.errors.title"
                                class="mt-1 text-sm text-red-600"
                            >
                                {{ form.errors.title }}
                            </div>
                        </form>

                        <!-- Todo List -->
                        <div
                            v-if="todos.length === 0"
                            class="text-center text-gray-500 dark:text-gray-400"
                        >
                            No todos yet. Create your first one above!
                        </div>

                        <div v-else class="space-y-2">
                            <div
                                v-for="todo in todos"
                                :key="todo.id"
                                class="flex items-center gap-3 rounded-lg border border-gray-200 p-3 dark:border-gray-700"
                            >
                                <!-- Checkbox -->
                                <input
                                    type="checkbox"
                                    :checked="todo.completed"
                                    @change="toggleComplete(todo)"
                                    class="h-5 w-5 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                                />

                                <!-- Todo Content (Edit mode or Display mode) -->
                                <div
                                    v-if="editingId === todo.id"
                                    class="flex-1 flex gap-2"
                                >
                                    <input
                                        v-model="editForm.title"
                                        type="text"
                                        class="flex-1 rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 dark:border-gray-700 dark:bg-gray-900"
                                        @keyup.enter="updateTodo(todo)"
                                        @keyup.esc="cancelEdit"
                                    />
                                    <button
                                        @click="updateTodo(todo)"
                                        class="rounded-md bg-green-600 px-3 py-1 text-sm text-white hover:bg-green-700"
                                    >
                                        Save
                                    </button>
                                    <button
                                        @click="cancelEdit"
                                        class="rounded-md bg-gray-600 px-3 py-1 text-sm text-white hover:bg-gray-700"
                                    >
                                        Cancel
                                    </button>
                                </div>

                                <div
                                    v-else
                                    class="flex-1 flex items-center justify-between"
                                >
                                    <span
                                        :class="{
                                            'line-through text-gray-500 dark:text-gray-400':
                                                todo.completed,
                                        }"
                                        class="cursor-pointer"
                                        @dblclick="startEdit(todo)"
                                    >
                                        {{ todo.title }}
                                    </span>

                                    <div class="flex gap-2">
                                        <button
                                            @click="startEdit(todo)"
                                            class="text-sm text-blue-600 hover:text-blue-800 dark:text-blue-400"
                                        >
                                            Edit
                                        </button>
                                        <button
                                            @click="deleteTodo(todo.id)"
                                            class="text-sm text-red-600 hover:text-red-800 dark:text-red-400"
                                        >
                                            Delete
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Stats -->
                        <div
                            v-if="todos.length > 0"
                            class="mt-4 text-sm text-gray-600 dark:text-gray-400"
                        >
                            {{ todos.filter((t) => !t.completed).length }} items
                            left
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
