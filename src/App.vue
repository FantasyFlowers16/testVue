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
import axios from "axios";
export default {
  name: 'App',
    data(){
      return {
      worker:[ ],
      urls: {
          ListUser: 'http://localhost:3000/api/v1/person/'
          },
      }

    },


    methods:{
      deleteWorker(id){
          axios.delete('http://localhost:3000/api/v1/person/'+id)

        //this.worker=this.worker.filter(t=>t.id!==id);
       // console.log(this.worker);

      }
  },
    mounted() {
        axios
            .get(this.urls.ListUser)
            .then(response => (this.worker=response.data))

    },
    components: {
    Workers,

  },


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
