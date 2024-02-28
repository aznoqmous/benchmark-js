<template>
<div class="editor">
    {{ name }}
    <CodeEditor value="" @keyup="update" ref="editor"></CodeEditor>
</div>
</template>

<script setup>
import hljs from 'highlight.js';
import CodeEditor from "simple-code-editor";
const editor = ref(null)
const props = defineProps(["index", "name", "content"])
const emits = defineEmits(["update"])
const content = ref("")
defineExpose({content})
const update =()=>{
    content.value = editor.value.content
    emits("update", props.index, editor.value.content)
}
</script>