<template>
    <div>
        <ul>
            <WorkerItem
              v-for="(w,i) of worker"

              v-bind:w="w"
              v-bind:ind="i"
              @delete-worker="deleteWorker"
            />
        </ul>

        <button class="btn" @click="showModal" > Добавить пользователя </button>
        <NewW
          v-show="isModalVisible"
          @close="closeModal"
          @new-worker="newWorker"
        />



    </div>
</template>
<script>
import  WorkerItem from '@/components/WorkerItem'
import NewW from '@/components/NewWorker'
import axios from "axios";

export default {
    props:['worker'],
    components:{
      WorkerItem,
      NewW,

    },
    data(){

      return {
        isModalVisible: false,
          error:[]

      };
    },
    methods:{
      deleteWorker(id){
        this.$emit("delete-worker",id);
          console.log(this.worker.length)

      },
      showModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
      },
      newWorker(w){
          axios.post('http://localhost:3000/api/v1/person/', w)
              .then((response) => {
                  console.log(response);
              })
              .catch((error) => {
                  console.log(error);
              });
      },


    }
}
</script>
<style scoped>
    ul{
      list-style: none;
      margin: 0;
      padding: 0;
      position: relative;
    }
    button{
      padding: 8px;
      margin:20px;
      margin-right: 10px;
      border: 2px solid #7b1313c7;
    }
</style>