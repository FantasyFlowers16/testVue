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
          error:[]
      }

    },



    methods:{
      deleteWorker(id){
          axios.delete(this.urls.ListUser+id)

      },
        getDataServ (count = 1, time = '', start) {
            axios
                .get(this.urls.ListUser)
                .then(response => (this.worker=response.data))
                .catch((err) => {
                    this.error = 'Error'
                })
        },
        stopTimer () {
            if (this.interval) {
                window.clearInterval(this.interval)
            }
        },
        startTimer () {
            this.stopTimer()
            this.interval = window.setInterval(() => {
                this.getDataServ()
            }, 500)
        }
    },

    mounted() {
        this.startTimer()

    },
    beforeDestroy () {
        this.stopTimer()
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
