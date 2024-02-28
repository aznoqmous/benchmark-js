<template>
    <Editor ref="setupEditor" name="Setup"/>
    <Editor v-for="test, index in tests" :index="index" :name="'Test ' + (index + 1)" @update="onUpdate"/>
    <button @click="addTest">
        Add test
    </button>
    <button @click="runTests">
        Run tests
    </button>
</template>
<script setup>
const setupEditor = ref(null)

const tests = ref([{
}])

const addTest = ()=>{
    tests.value.push({
    })
}

const onUpdate = (index, content)=>{
    tests.value[index].content = content
}

const _test = ()=>{
    /*setup*/
    for(let _i = 0; _i < this.iterations; _i++){
        const last = performance.now()
        for(let _l = 0; _l < this.loops; _l++){
            /*test*/
        }
        this.times.push(performance.now() - last)
    }
}
const runTest = (setup, test, loops=1, iterations=1)=>{
    const body = _test.toString()
    .replace("/*setup*/", setup.toString())
    .replace("/*test*/", test.toString())
    .split("\n")
    body.splice(0,1)
    body.splice(-1,1)
    let times = []
    Function(body.join("\n")).bind({
        loops, 
        iterations,
        times
    })()
    return {
        times
    }
}

const runTests = ()=>{
    const loops = 1000;
    const iterations = 1000;

    const setupTest = setupEditor.value.content

    eval(setupEditor.value.content)

    tests.value.map(test => {
        test.times = runTest(setupTest, test.content, iterations, iterations).times
    })

    tests.value.map(test => {
        console.log((test.times.reduce((p,v)=> p+v)/iterations/loops).toFixed(8) + "ms")
    })
}




</script>
