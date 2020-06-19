<template>
  <div id="app">
   <h1>Список сотрудников</h1>
      <hr>
    <Workers
    v-if="worker.length"
    v-bind:worker="worker"
    @delete-worker="deleteWorker"
    />
    <p v-else>Список сотрудников отсутствует.</p>
  </div>
</template>

<script>
import Workers from '@/components/Workers'
export default {
  name: 'App',
    data(){
      return{
        worker:[],

      }
    },
    mounted() {
        fetch('https://jsonplaceholder.typicode.com/users')
          .then(response => response.json())
          .then(json =>{
            this.worker=json;
            console.log(json);
          })
    },
    methods:{
      deleteWorker(id){
        this.worker=this.worker.filter(t=>t.id!==id)
      },

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
