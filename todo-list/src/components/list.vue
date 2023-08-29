<template>
    <main>
        <div class="input">
            <input type="text" placeholder="Create a new todo..." id="text" v-model="newTask" @keyup.enter="addTask">
        </div>
        <div class="all">
            <ul class="all-tasks">
                <Tasks v-for="(task, index) in tasks" :key="index"  :tasks="task" @deleteTasks="deleteTask(index)" ></Tasks>
            </ul>
            
            <ul class="filter">
            <li class="filter-item"> 5 items left</li>
            <li class="filter-item">All</li>
            <li class="filter-item">Active</li>
            <li class="filter-item">Completed</li>
            <li class="filter-item">Clear Completed</li>
            </ul>
        </div>


    </main>
</template>

<script>
import Tasks from './tasks.vue'

export default{
    components:{
        Tasks
    },
    data(){
        return{
            newTask: '',
            tasks: [],
    
        };
    },
    methods:{
        addTask(){
            if (this.newTask.trim() !== ''){
                this.tasks.push(this.newTask);
                this.newTask = '';
            }
        },
        deleteTask(index){
            this.tasks.splice(index, 1);
        },
    }
}

</script>

<style scoped>
main{
    background-color:transparent;
    color: black;
}
.all{
    background: white;
    margin-top: 10px;
    border-radius: 15px;
    padding: 5px;
}
.input{
    padding: 5px;
    border-radius: 10px;
    background: white;
    
}
input{
    border: none;
    width: 70vw;
    padding: 20px;

}
input:focus{
    outline: none;
    
}
.all-tasks{
    
    padding: 5px;
    background-color:white ;
}
.filter{
    display: flex;
    
    padding: 15px;
    justify-content: space-evenly;
}
.filter-item{
    list-style: none;
    font-size: 13px;
}
</style>