<template>
  <div id="app">
   <h1>Сотрудники</h1>
    <Workers
    v-bind:worker="worker"
    @delete-worker="deleteWorker"

    />

  </div>
</template>

<script>
import Workers from '@/components/Workers'


export default {
  name: 'App',
    data(){
      return{
          worker:[],
          isModalVisible: false
      }
    },

    methods:{
      deleteWorker(id){
          this.worker=this.worker.filter(t=>t.id!==id)
      },
      showModal() {
          this.isModalVisible = true;
      },
      closeModal() {
          this.isModalVisible = false;
      }

  },
  components: {
    Workers


  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
