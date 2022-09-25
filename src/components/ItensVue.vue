<template>
  <div id="CorpoCyberVerse">
      <span >
          <h1 id="TitleCyber">{{book.id}}.{{book.title}}</h1>
          <img id="ImageItem" :src="book.image" alt="">
          <p id="Descrição">{{book.Descri}}</p>
          <i class="Editar" @click="$emit('edit-book-item', book.id)">edit</i>
          <i class="Apagar" @click="$emit('del-book-item', book.id)">delete</i>
      </span>
  </div>
</template>

<script>
  export default {
      name: "ItensVue",
      props: ["book"]
  }
</script>
