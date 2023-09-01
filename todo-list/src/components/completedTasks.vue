<template>
    <ul>
        <li v-for="(task, index) in listCompleted " :key="index">
            {{ task }}

        </li>
    </ul>
</template>

<script>
export default{
    props:{
        listCompleted:Array
    }
    
}

</script>