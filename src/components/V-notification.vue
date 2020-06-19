<template>
    <div class="v-notification">
        <div class="v-notification.content"
             v-for="message in massages"
             :key="message.id">
            <div class="content-text">
            <span>Notification text</span>
            </div>
        </div>
        <div class="notification.button">
            <button>Ok</button>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'v-notification',
        props:{
            message:{
                type: Array,
                default:()=>{
                  return []
                }

            }
        },
    }

</script>
<style>
    .v-notification{
      position: fixed;
      margin:auto;
      left:0;
      right:0;
      bottom: 5px;
      z-index: 10;
      width: 250px;
      min-height:70px;
      border:2px solid #8c1010ab;
      border-radius: 6px;
      background:#d25f5fa6;
    }
    .v-notification.content{
      border-radius: 4px;
      color:white;
      display: flex;
      justify-content: space-between;
      height: 50px;
      margin-bottom: 10px;
    }

</style>