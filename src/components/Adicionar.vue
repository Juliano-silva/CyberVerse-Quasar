<template>
  <div class="Corpo" id="AdicionarCorpo">
      <form @submit="addBook">
          <input type="text" name="title" v-model="title" placeholder="Titulo" required> <br>
              <input type="text" name="image" v-model="image" placeholder="Imagem"> <br>
              <input type="text" name="Descri" v-model="Descri" placeholder="Descrição" required> <br>
              <input type="submit" value="Enviar">
      </form>
  </div>
</template>

<script>
  export default {
      name: "AdicionarVue",
      props: ['editBook'],
      data () {
          return {
              title: '',
              image:'',
              Descri:'',
              id: '',
              edit: false
          }
      },
      methods: {
          addBook(e){
              e.preventDefault();
              if (this.edit === false){
                  // add new book
                  const newBook = {
                      title: this.title,
                      image: this.image,
                      Descri: this.Descri,
                      id: Math.floor(Math.random() * 100)
                  };
                  if (newBook.title !== ''){
                      this.$emit('add-book-event', newBook);
                  }
                  this.image = '',
                  this.Descri = '',
                  this.title = ''
              }else{
                  //edit book
                  const bookItem = {
                      title: this.title,
                      image: this.image,
                      Descri: this.Descri,
                      id: this.id
                  };
                  //send to parent (App.vue)
                  this.$emit('edit-book-event', bookItem);
                  // clear input field
                  this.title = '';
                  this.image = '';
                  this.Descri = '';
                  this.edit = false;
              }
          }
      },
      watch: {
          editBook: {
            // Editar Botão
              handler() {
                  this.title = this.editBook.title;
                  this.image = this.editBook.image;
                  this.Descri = this.editBook.Descri;
                  this.id = this.editBook.id;
                  this.edit = true
              },
              deep: true
          },
          title:{
              handler(){
                  if(this.title === '', this.image === '' , this.Descri === ''){
                      this.edit = false;
                  }
              }
          }
      }
  }
</script>

