<template>
    <ul>
        <li v-for="(task, index) in listActive" :key="index">
            {{ task }}
            <div class="line"></div>
        </li>
    </ul>
</template>

<script>
export default{
    props:{
        listActive: Array
    }
}

</script>
<style scoped>
    ul{
        background: white;
        margin-top: 10px;
        border-radius: 15px;
        padding: 5px;
        width: 70vw;
    }
    .line{
    height: 1px;
    background-color:hsl(236, 9%, 61%);
    margin-block: 10px;

}

    li{
        list-style: none;
        list-style: none;
        font-size: 21px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }

</style>