<template>
<div class="editor">
    Test n°{{ index + 1 }}
    <CodeEditor value="" @keyup="update" ref="editor"></CodeEditor>
</div>
</template>

<script setup>
import hljs from 'highlight.js';
import CodeEditor from "simple-code-editor";
const editor = ref(null)
const props = defineProps(["index", "content"])
const emits = defineEmits(["update"])

const update =()=>{
    emits("update", props.index, editor.value.content)
}
</script>