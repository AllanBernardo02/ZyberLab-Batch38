<template>

    <q-toolbar class="bg-purple text-white">
      <q-btn flat round dense icon="assignment_ind" />
      <q-toolbar-title>
          {{state.task}}
        Batch 38 TODO App
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
        <q-item clickable v-ripple>
            <q-item-section avatar>
                <q-icon name="signal_wifi_off" />
            </q-item-section>
            <q-item-section>{{todo.desc}}</q-item-section> <!-- todo.desc called data binding-->
            <q-item-section side>Side</q-item-section>
        </q-item>
    </q-list>
    
   
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

 




</template>

    <!-- composition API -->
<script setup>

import { reactive, ref } from 'vue'

//Using Reactive
const state = reactive({
            task: ''
    //         todos: [
    //         {
    //             id: Date.now(),
    //             desc: 'add function',
    //             isDone: false
    //         }
    // ]
    })

//Using ref
const todos = ref([
            {
                id: Date.now(),
                desc: 'add function',
                isDone: false
            }
    ])


    function add() 
    {
        //If we use reactive, use state like this.. state.todos.push({object:object})
        //if we use ref, use .value like this.. todos.value.push({object:object})
        todos.value.unshift(
            {
                id: Date.now(),
                desc: state.task,
                isDone: false
            }
        );
        state.task = ""; //it is for clearing text or data in input
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