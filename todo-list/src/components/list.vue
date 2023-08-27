<template>
    <main>
        <div class="input">
            <input type="text" placeholder="Create a new todo..." id="text" v-model="newTask" @keyup.enter="addTask">
        </div>
        <ul>
            <Tasks :tasks="tasks"></Tasks>
        </ul>
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
                this.newTask = ''
            }
        }
    }
}

</script>

<style scoped>
main{
    background-color:transparent;
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
ul{
    border-radius: 5px;
    padding: 5px;
    background-color:white ;
    margin-top:20px ;
}
</style>