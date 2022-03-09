<template>

    <q-toolbar class="bg-purple text-white">
      <q-btn flat round dense icon="assignment_ind" />
      <q-toolbar-title>
        Batch 38 TODO App
      </q-toolbar-title>
      <q-btn flat round dense icon="apps" class="q-mr-xs" />
      <q-btn flat round dense icon="more_vert" />
    </q-toolbar>

    <div class="row  q-gutter-sm  q-pa-sm">
        <q-input class="col" filled v-model="text" label="What needs to be done" />
        <q-btn icon="add" label="add"></q-btn>
   </div>
    <q-list class="q-ma-sm" bordered separator>
        <!-- first list -->
        <q-item clickable v-ripple>
            <q-item-section avatar>
                <q-icon name="signal_wifi_off" />
            </q-item-section>
            <q-item-section>Active</q-item-section>
            <q-item-section side>Side</q-item-section>
        </q-item>
        <!-- Second list -->
        <q-item clickable v-ripple>
            <q-item-section avatar>
                <q-icon name="signal_wifi_off" />
            </q-item-section>
            <q-item-section>Active</q-item-section>
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