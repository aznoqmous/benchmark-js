<template>

    <Editor v-for="test, index in tests" :index="index" @update="onUpdate"/>
    <button @click="addTest">
        Add test
    </button>
    <button @click="runTests">
        Run tests
    </button>
</template>
<script setup>
const tests = ref([{
}])

const addTest = ()=>{
    tests.value.push({
    })
}

const onUpdate = (index, content)=>{
    tests.value[index].content = content
}

const runTests = ()=>{
    const loops = 100;
    const iterations = 100;

    tests.value.map(test => {
        test.times = []
    })

    for(let i = 0; i < iterations; i++){
        tests.value.map(test => {
            const start = performance.now()
            for(let i = 0; i < loops; i++) eval(test.content)
            test.times.push(((performance.now() - start) / loops))
        })
    }

    tests.value.map(test => {
        console.log((test.times.reduce((p,v)=> p+v)/iterations).toFixed(4) + "ms")
    })
}


</script>
