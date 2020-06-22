<template>
    <li>
      <div class="first">
        {{ind+1}}
        {{w.firstname}}
        {{w.lastname}}
      </div>
        <div class="second">
          <button @click="showModal"
          >...</button>
          <button class="delete" v-on:click="$emit('delete-worker',w.id)">&times;</button>
        </div>
      <modal
              v-show="isModalVisible"
              @close="closeModal"
              v-bind:beforeFirstname="w.firstname"
              v-bind:beforeLastname="w.lastname"
              @correction="correctionData"
      />

    </li>
</template>
<script>
import modal from '@/components/CorrectWorker'
import axios from "axios"
export default {

    props:{
        w:{
          type:Object,
          required: true,
        },
        ind:Number,
        firstname:String,
        lastname:String,
    },
  data(){
    return {
      isModalVisible: false,
      urls: {
        ListUser:'http://localhost:3000/api/v1/person/'
      },
    }
  },
  components:{
    modal
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    correctionData(CorrectWorker){
      axios.put(this.urls.ListUser+this.w.id,CorrectWorker);
    }
  },
}
</script>
<style scoped>
    li{
      position: relative;
      border: 1px solid #80050552;
      border-radius: 14px;
      padding: 10px;
      background: beige;
      display: flex;
      margin-bottom: 3px;
      z-index: 0;
    }
    .first{
      display: flex;
      flex: 6;
    }
    .second{
      display: flex;
      flex: none;
      width: 5em;
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