<script setup>
import { Head, Link } from "@inertiajs/vue3";
import { Editor, EditorContent, useEditor } from "@tiptap/vue-3";
import StarterKit from "@tiptap/starter-kit";

const editor = useEditor({
    editorProps: {
        attributes: {
            class: "border border-gray-400 min-h-[12rem] max-h-[12rem] overflow-y-auto outline-none",
        },
    },
    content: "<p>I’m running Tiptap with Vue.js. 🎉</p>",
    extensions: [StarterKit],
});
</script>

<template>
    <Head title="Welcome" />
    <div class="container mx-auto max-w-4xl my-8">
        <section
            v-if="editor"
            class="buttons flex items-center flex-wrap gap-x-4 border border-l border-t border-r border-gray-400 p-4"
        >
            <button
                @click="editor.chain().focus().toggleBold().run()"
                :disabled="!editor.can().chain().focus().toggleBold().run()"
                :class="{
                    'bg-gray-300 is-active p-1 rounded-md':
                        editor.isActive('bold'),
                }"
            >
                bold
            </button>

            <button @click="editor.chain().focus().setHorizontalRule().run()">
                horizontal rule
            </button>
        </section>
        <EditorContent :editor="editor" />
    </div>
</template>
