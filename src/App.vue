<template>
  <div class="container">
    <h1 class="title">Comentários</h1>

    <CommentsForm v-on:form-data="handleCommentInsertion" />

    <hr>

    <section class="section">
      <p v-if="comments.length <=0">Sem comentários...</p>
        <div
            class="card"
            v-for="(commentData, index) in allComments"
            v-bind:key="index"
        >
          <div class="card-content">
            <div class="content">
              <strong>Autor:</strong>
              <span>{{commentData.user}}</span>
            </div>
  
            <div class="content">
              <strong>Comentário</strong>
              <span>{{commentData.message}}</span>
            </div>
          </div>

          <button class="button is-danger is-small" v-on:click="handleCommentDelete(index)">
            Excluir
          </button>

          <hr />
        </div>
    </section>
  </div>
</template>

<script>
  import CommentsForm from './components/CommentsForm.vue';

  export default {
    name: 'App',

    components: {
      CommentsForm,
    },

    data() {
      let storageComments = this.getCommentsFromStorage();

      if (!storageComments) {
        storageComments = [];
      }

      return {
        comments: storageComments,
      };
    },

    methods: {
      handleCommentInsertion(comment) {
        this.comments.unshift(comment);
      },

      handleCommentDelete(commentIndex) {
        this.comments.splice(commentIndex, 1);
      },

      getCommentsFromStorage() {
        const comments = JSON.parse(localStorage.getItem('saved-comments'));

        return comments;
      },

      setCommentsToStorage() {
        localStorage.setItem('saved-comments', JSON.stringify(this.comments));
      }
    },

    computed: {
      allComments() {
        return this.comments.map(comment => ({
          ...comment,
          user: comment.user.trim() === '' ? 'Anônimo' : comment.user
        }));
      }
    },

    watch: {
      comments() {
        this.setCommentsToStorage();
      }
    }

  }
</script>