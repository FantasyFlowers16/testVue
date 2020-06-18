<template>
    <div class="modal-backdrop">
        <div class="modal">
            <header class="modal-header">
                <slot name="header">
                        Добавление нового сотрудника
                </slot>
            </header>
            <section class="modal-body">
                <slot name="body">
                    <p><b>Имя:</b><br>
                        <input type="text" size="40" v-model="name"></p>
                    <p><b>Фамилия:</b><br>
                        <input type="text" size="40" v-model="surname"></p>

                </slot>
            </section>
            <footer class="modal-footer">
                <slot name="footer">
                    <button
                            type="button"
                            class="btn-close"
                            @click.prevent="close"
                    >
                        Отмена
                    </button>
                    <button
                            type="button"
                            class="btn-save"
                            @click="onSave"
                    >
                        Сохранить
                    </button>
                </slot>
            </footer>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'modal',
    data(){
        return{
            name:'',
            surname:''
        }
    },
        methods: {
            close() {
                this.$emit('close');
            },
            onSave(){
               console.log('save',this.name,this.surname)
                if (this.name.trim()){
                    if (this.surname.trim()){
                        const newWorker= {
                            id: Date.now(),
                            name: this.name,
                            surname: this.surname
                        }
                        this.$emit('new-worker',newWorker)
                        this.surname='';
                        this.name='';
                    }
                }
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
    }

    .modal-header,
    .modal-footer {
        padding: 15px;

    }

    .modal-header {
        border-bottom: 1px solid #eeeeee;
        color: #590303;
        justify-content: space-between;
    }

    .modal-footer {
        border-top: 1px solid #eeeeee;
        justify-content: flex-end;
    }

    .modal-body {
        position: relative;
        padding: 60px 30px;
    }


    .btn-close {
        color: black;

        border: 1px solid black;
        border-radius: 2px;
    }
    .btn{
        margin: 10px;
    }
</style>