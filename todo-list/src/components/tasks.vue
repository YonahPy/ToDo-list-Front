<template>
    <ul class="tasks">
        
        <li v-for="(task, index) in tasks" :key="index">
            <button id="check" @click="checkTask" :class="{'checked': isChecked}">
            <img src="../../public/images/icon-check.svg" alt="check" id="image-checked" >
            </button>

        {{ task }}
        <button id="delete" @click="deleteTask">
            <img src="../../public/images/icon-cross.svg" alt="delete">
        </button>

        </li>

    </ul>
</template>

<script>
export default{
    data(){
        return{
            isChecked: false
        }
    },
    props:{
        tasks:Array
    },
    methods:{
        checkTask(){
            this.isChecked = !this.isChecked
            const li = document.getElementById('item');
            const img = document.getElementById('image-checked')
            if (this.isChecked){
                li.style.textDecoration = 'line-through'
                img.style.display = 'inline'
                li.style.color = 'gray'
            }else{
                li.style.textDecoration = ''
                img.style.display = 'none'
                li.style.color = ''
            }


        },
        deleteTask(){
            const tasks = document.querySelector('.tasks');
            tasks.remove()
        }
    }
    
}
</script>

<style scoped>
:root {
  --check-gradient: linear-gradient(to bottom right, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}
.tasks{
    display: flex;
    width: 70vw;
    background-color: white;
    padding: 15px;
    
}
li{
    list-style: none;
    font-size: 21px;
}

#check{
    border-radius: 50%;
    border: 1px solid hsl(192, 100%, 67%);
    width: 23px;
    height: 23px;
    margin-right: 10px;
    
}
.checked{
    background: linear-gradient(to bottom right, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}
#check img{
    display: none;
}

#delete{
    width: 23px;
    height: 23px;
    border: none;
    font-size: 25px;
    background-color: transparent;
    margin-left: auto;
    opacity: 0;
    transition: opacity 0.2s ease, visibility 0.3s ease;
}
.tasks:hover #delete{
    visibility: visible; 
    opacity: 1;
}

</style>

