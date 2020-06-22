<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal-header">
                    <slot name="header">Редактирование сотрудника </slot>
                </header>
                <section class="modal-body">
                    <slot name="body">
                        <p><b>Имя:</b><br>
                            <input type="text" size="40" v-model="firstname" ></p>
                        <p><b>Фамилия:</b><br>
                            <input type="text" size="40" v-model="lastname" ></p>

                    </slot>
                </section>
                <footer class="modal-footer">
                    <slot name="footer">
                        <button class="btn-close" @click.prevent="close">Отмена</button>
                        <button class="btn-save" @click="onSave"@click.prevent="close">Сохранить</button>
                    </slot>
                </footer>
            </div>
        </div>
    </transition>
</template>
<script>
import message from '@/notification/vue-notification'
export default {

    props:['count','beforeFirstname','beforeLastname'],
    data(){
        return{
            firstname:this.beforeFirstname,
            lastname:this.beforeLastname
        }
    },
    methods: {
        close() {
            this.$emit('close');
        },
        onSave(){
            if (this.firstname === '' || this.lastname === ''){
                this.$toasted.error(message['empty'],{ position:'bottom-center'}).goAway(4000)
            }
             else if(this.firstname!==this.beforeFirstname || this.lastname!==this.beforeLastname)   {
                const CorrectWorker = {
                    firstname: this.firstname,
                    lastname: this.lastname,
                 }
                this.$toasted.success(message['saveChange'],{ position:'bottom-center'}).goAway(4000)
                 this.$emit('correction',CorrectWorker)
            }else this.$toasted.info(message['notUse'],{ position:'bottom-center'}).goAway(4000)

        }
    }
};
</script>
<style>
    .modal-backdrop {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        background: #FFFFFF;
        box-shadow: 2px 2px 20px 1px;
        overflow-x: auto;
        display: flex;
        flex-direction: column;
        border-radius: 15px;
        z-index: 999999;

    }

    .modal-header,
    .modal-footer {
        padding: 15px;
    }

    .modal-header {
        border-bottom: 1px solid #dcb8b8;
        color: #590303;
        justify-content: space-between;
        font-size: 14pt;
        font-family:"GeorgiaAvenir, Helvetica, Arial, sans-serif",serif;
        background: #ece2e2;
    }

    .modal-footer {
        border-top: 1px solid #eeeeee;
        justify-content: flex-end;
    }

    .modal-body {
        position: relative;
        padding: 60px 30px;
        font-family:"GeorgiaAvenir, Helvetica, Arial, sans-serif",serif;
        z-index: 10;
    }


    .btn-close {
        padding: 4px;
        margin: 4px;
        border-radius: 10px;
        color: #2c3e50;
        border-color:#80050587;
        outline:none;
    }

    button{
        padding: 4px;
        margin: 4px;
        border-radius: 10px;
        color: #2c3e50;
        border-color:#80050587;
        outline:none;
    }
    button:hover {
        background: #ecdcdc;
        cursor: pointer;
    }
    .modal-fade-enter,
    .modal-fade-leave-active {
        opacity: 0;
    }

    .modal-fade-enter-active,
    .modal-fade-leave-active {
        transition: opacity .10s ease;
    }
</style>