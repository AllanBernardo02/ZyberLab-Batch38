<template>
    <div>
    <q-toolbar class="bg-purple text-white">
      <q-btn flat round dense icon="assignment_ind" />
      <q-toolbar-title>
          {{state.task}} 
        Batch 38 TODO App 
        <greet v-if="!state.fullName" @getFullName="(val) => state.fullName = val" fname="Allan" lname="Bernardo"/>
        <span v-else>{{state.fullName}}</span>
      </q-toolbar-title>
      <q-btn flat round dense icon="apps" class="q-mr-xs" />
      <q-btn flat round dense icon="more_vert" />
    </q-toolbar>

    <div class="row  q-gutter-sm  q-pa-sm">
        <q-input @keyup.enter="add" v-model="state.task" class="col" filled  label="What needs to be done" />
        <q-btn @click="add" icon="add" label="add"></q-btn>
   </div>
    <q-list v-for="todo in todos" :key="todo.id" class="q-ma-sm" bordered separator>
        <!-- first list -->
        <q-item clickable v-ripple @mouseover="selected = todo.id" @mouseleave="selected = null">
            <q-item-section avatar>
                <q-checkbox v-model="todo.completed" />
            </q-item-section>
            <q-item-section :class="{ 'text-strike text-grey':  todo.completed}">{{todo.title}}</q-item-section> <!-- todo.desc called data binding-->
            <q-item-section side>
                <q-btn v-show="selected === todo.id" round icon="delete"/>
            </q-item-section>
        </q-item>
    </q-list>
    <pie-chart :data="[['Active', countActive], ['Completed', countCompleted]]"></pie-chart>
    
    <q-btn icon="print" @click="print"/>
    <q-btn icon="download" @click="download"/>
    <q-btn icon="email" @click="open"/>
   
    <!-- <div class="todos">
        <q-toolbar class="bg-purple text-white">
      <q-btn flat round dense icon="assignment_ind" />
      <q-toolbar-title>
        Batch 38 TODO App
      </q-toolbar-title>
      <q-btn flat round dense icon="apps" class="q-mr-xs" />
      <q-btn flat round dense icon="more_vert" />
    </q-toolbar>
        <input @keyup.enter="add" type="text" v-model="title" placeholder="What you want todo">
        <button @click="add">Add to list</button>

        <ul>
            <li style="list-style-type: none" v-for="todo in todos" :key="todo"><q-btn style="width: 50%; margin: auto"><input type="checkbox"><label for="">{{todo}}</label></q-btn></li>
            <li v-for="todo in todos">{{todo}}</li>
        </ul>

    </div> -->

 



</div>
</template>

    <!-- composition API -->
<script setup>

import { reactive, ref, onMounted, computed, getCurrentInstance } from 'vue' //getCurrentInstance use if u get axios globally
// import axios from 'axios' // Option 1 for using axios: To get data into server

import greet from 'components/greet.vue'

const app = getCurrentInstance()

const { $axios, $pdfMake } =app.appContext.config.globalProperties // Option 2 for using axios globally:

//Using Reactive
const state = reactive({
            task: '',
            fullName: ''
    //         todos: [
    //         {
    //             id: Date.now(),
    //             desc: 'add function',
    //             isDone: false
    //         }
    // ]
    })

const countCompleted = computed(() => todos.value.filter(t => t.completed).length)// To compute all todos.value if completed.. sample value is 6
const countActive = computed(() => todos.value.length - countCompleted.value) // To compute all todos.value in array then minus in the completed.value

const selected = ref(null) // for hover delete icon

const list = computed(() => todos.value.length)
//Using ref
const todos = ref([
            {
                id: Date.now(),
                title: 'add function',
                completed: false
            }
    ])

// onMounted is to initialize the data from axios and Axios used to get the into server
onMounted(async () => {
    const { data } = await /*axios or*/$axios.get("https://jsonplaceholder.typicode.com/todos"); //if we use global axios by default use $axios, else axios
    todos.value = data;
})

    function add() 
    {
        //If we use reactive, use state like this.. state.todos.push({object:object})
        //if we use ref, use .value like this.. todos.value.push({object:object})
        todos.value.unshift(
            {
                id: Date.now(),
                title: state.task,
                completed: false
            }
        );
        state.task = ""; //it is for clearing text or data in input
    }

    function print() {
        const dd = {
            content: [
                {
                    table: {
                        body: [
                            ['completed', 'active', 'All_list'],
                            [countCompleted.value, countActive.value, list.value]
                        ]
                    }
                }
            ]
        }
        $pdfMake.createPdf(dd).print()
    
    }

    function download() {
        const dd = {
            content: [
                {
                    table: {
                        body: [
                            ['completed', 'active'],
                            [countCompleted.value, countActive.value]
                        ]
                    }
                }
            ]
        }
        $pdfMake.createPdf(dd).download()
    }

    function open() {
        const dd = {
            content: [
                {
                    table: {
                        body: [
                            ['completed', 'active'],
                            [countCompleted.value, countActive.value]
                        ]
                    }
                }
            ]
        }
        $pdfMake.createPdf(dd).open()
    }
        
</script>



   
<!-- <script>
    export default {
        name: "todo",
        props: {
            msg: String
        },
        data(){
            return {
                title: '',
                todos:[
                    // 'Go to Shop'
                ]
            }
        },
        methods:{
            add(){
                this.todos.push(this.title);
                this.title = "";
            }
        }
    };
    
</script> -->

<!-- <script>
    export default {
        data: () => ( //nagrereturn ng value
            {
                task: '',
                todos:[]
            }
        ),

        methods: {
            add() {
                this.todos.unshift({
                    id: Date.now(),
                    decs: this.task,
                    isDone: false

                })
            },
            remove() {},
            update() {},
        }
    }
</script> -->