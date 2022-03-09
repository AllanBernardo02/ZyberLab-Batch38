<template>
    <div>
        hello {{lname}}
        <q-btn @click="getFullName">Get Fullname</q-btn>
    </div>
</template>

<script setup>
    import { defineProps, toRefs, defineEmits } from 'vue'
    
    const props = defineProps({
        fname: String,
        lname: String
    })
    console.log(toRefs(props));
    const {fname, lname} = toRefs(props)

     const emit = defineEmits()

    function getFullName (){
        emit('getFullName', fname.value + '' + lname.value)
    }
    // const {name} = toRefs(props)
</script>