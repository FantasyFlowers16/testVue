<template>
    <li>
        {{ind+1}}
        {{w.name}}
        {{w.surname}}
        <button >Редактировать
        </button>
        <button class="delete" v-on:click="$emit('delete-worker',w.id)">&times;</button>

    </li>

</template>
<script>

export default {
    props:{
        w:{
            type:Object,
            required: true,

        },
        ind:Number
    },



}
</script>
<style scoped>
    li{
        border: 1px solid #800505;
        border-radius: 14px;
        padding: 10px;
        background: beige;
        display: flex;
        justify-content:space-around;
    }
</style>