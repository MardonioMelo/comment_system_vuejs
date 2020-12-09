<template>
    <div class="form-todo form-group">
        <p>
            <input v-model="name" type="text" placeholder="Nome" name="author" class="form-control">
        </p>
        <p>
            <textarea v-model="message" name="message" placeholder="Comentário" class="form-control"></textarea>
        </p>
        <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: "",
            message: ""
        }
    },
    methods: {
          //Método executado quando o botão e clicado
        addComment() {
            //Verifica se o campo mensagem está vazio e não retorna nada
            if (this.message.trim() === '') {
                return;
            }
           
           this.$emit('add-todo', {
               name: this.name,
               message: this.message
           })


            this.name = '';
            this.message = '';        
        },
    },
}
</script>