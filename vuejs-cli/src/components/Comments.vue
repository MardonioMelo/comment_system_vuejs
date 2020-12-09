<template>
    <!-- Template do formulário -->
    <div class="container">
        <h1>Comentários</h1>
        <hr />
        <FormTodo v-on:add-todo="addComment"></FormTodo>
        <div class="list-group">
        <p v-if="comments.length <= 0">Sem comentários...</p>
        <div v-else class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
            <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>
            <p>{{ comment.message }}</p>
            <div>
                <a href="#" v-on:click.prevent="removeComment(index)" title="Excluir">Excluir</a>
            </div>
        </div>           
        </div>
    </div>
</template>

<script>
import FormTodo from './FormTodo';
export default {
   components:{
       FormTodo
   },
    data() {
        //Dados armazenado
        return {
            comments: [],         
        }
    },
    methods: {   
        addComment(comment){
            this.comments.push(comment);
        },    
        //Função para remover um comentário conforme seu índice
        removeComment(index) {
            this.comments.splice(index, 1)
        }
    }, //Usando para logica, verifica se o nome está vazio e preenche o valor com uma string padrão
    computed: {
        allComments(){
            return this.comments.map(comment => ({
                ...comment,
                name: comment.name.trim() === ''? 'Anônimo' : comment.name
            }))
        }
    }, // Usando para monitorar uma fonte de dados e executar uma ação, por exemplo salvar os dados no banco de dados.
    watch:  {             
        allComments: function (val){
            console.log('val',val)
        }
    }
}
</script>