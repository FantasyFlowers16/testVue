<template>
    <div>
        <ul>
            <WorkerItem
              v-for="(w,i) of worker"
              v-bind:w="w"
              v-bind:ind="i"
              v-on:delete-worker="deleteWorker"
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

export default {
    props:['worker'],
    components:{
      WorkerItem,
      NewW,
    },
    data () {
      return {
        isModalVisible: false,
      };
    },
    methods:{
      deleteWorker(id){
        this.$emit("delete-worker",id);
      },
      showModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
      },
      newWorker(w){
        this.worker.push(w);
      }
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
      position: absolute;
      border: 1px solid black;
    }
</style>