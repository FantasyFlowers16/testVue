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

        <button class='btn' @click='showModal' > Добавить пользователя </button>
        <NewW
          v-bind:count="worker[worker.length]"
          v-show='isModalVisible'
          @close='closeModal'
          @new-worker='newWorker'
        />
    </div>
</template>
<script>
import  WorkerItem from '@/components/WorkerItem'
import NewW from '@/components/NewWorker'
import axios from "axios";
import message from '@/notification/vue-notification'


export default {
    props:['worker'],
    components:{
      WorkerItem,
      NewW,

    },
    data(){

      return {
        isModalVisible: false,
          urls: {
              ListUser: 'http://localhost:3000/api/v1/person/'
          },
        error:[],
      };
    },
    methods:{
      deleteWorker(id){
        this.$emit('delete-worker',id);
         this.$toasted.success(message['deleteWorker'],{ position:'bottom-center'}).goAway(4000)
      },
      showModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
      },
      newWorker(w){
          axios.post(this.urls.ListUser, w)
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