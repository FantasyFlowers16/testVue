<template>
    <li>
      <div class="first">
        {{ind+1}}
        {{w.firstname}}
        {{w.lastname}}

      </div>
        <div class="second">
          <button>Редактировать</button>
          <button class="delete" v-on:click="$emit('delete-worker',w.id)">&times;</button>
        </div>
    </li>
</template>
<script>
export default {
    props:{
        w:{
          type:Object,
          required: true,
        },
      data(){
         return{
           firstname:'',
           lastname:''
         }

      },
        ind:Number,
        firstname:String,
        lastname:String
    },
  data(){
    return {

    }
  },

}
</script>
<style scoped>
    li{
      position: relative;
      text-align: left;
      border: 1px solid #80050552;
      border-radius: 14px;
      padding: 10px;
      background: beige;
      display: flex;
      margin-bottom: 3px;
    }
    .first{
      display: flex;
      flex: 3;
    }
    .second{
      display: flex;
      flex: none;
      width: 10em;
    }
    button{
      padding: 4px;
      margin: 4px;
      border-radius: 7px;
      color: #2c3e50;
      border-color:#80050587;
      outline:none;
    }
    button:hover{
      background: #ecdcdc;
      cursor: pointer;
    }
</style>