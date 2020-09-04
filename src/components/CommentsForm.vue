<template>
    <section class="section">
        <form class="form" v-on:submit.prevent="handleFormSubmit">
            <div class="field">
                <label class="label" for="name">Usuário</label>
                <input
                    class="input"
                    type="text"
                    placeholder="Seu nome"
                    name="name"
                    v-model="user"
                >
            </div>

            <div class="field">
                <label class="label" for="name">Comentário</label>
                <input
                    class="input"
                    type="text"
                    placeholder="Digite um comentário"
                    name="name"
                    v-model="message"
                >
            </div>

            <div class="hero">
                <button
                    class="button is-success"
                    type="submit"
                >
                    Comentar
                </button>
            </div>
        </form>
    </section>
</template>

<script>
    export default {
        name: 'CommentsForm',

        data() {
            return {
                user: '',
                message: ''
            };
        },

        methods: {
            handleFormSubmit() {
                if (this.message.trim() === '') return;

                this.$emit('form-data', {
                    user: this.user,
                    message: this.message
                });

                this.user = '';
                this.message = '';
            }   
        }
    }
</script>