
<template lang="html">

  <div class="container">
    <div class="row">
      <div class="col">

        <h3>¿Estás seguro qué deseas eliminar este libro?</h3>
        <p>Titulo: {{this.element.title}}</p>
        <p>Descripción: {{this.element.description}}</p>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <b-button v-on:click="deleteBook" variant="danger">Eliminar</b-button>
      </div>
    </div>
  </div>




</template>

<script>
import axios from 'axios';
import swal from 'sweetalert';

export default {
  data(){
    return{
      bookId: this.$route.params.bookId,
      element: {
        title: '',
        description: ''
      }
    }
  },
  methods:{

    getBook(){
      const path =`http://localhost:8000/api/v1.0/books/${this.bookId}/`
        axios.get(path).then((responser)=>{
          this.element.title = responser.data.title;
          this.element.description = responser.data.description;
        }).catch((error)=>{
          console.log(error);
        })
    },
    deleteBook(){
      const path =`http://localhost:8000/api/v1.0/books/${this.bookId}/`
        axios.delete(path).then((responser)=>{
          location.href = '/books';
          //swal('Libro eliminado', 'El libro ha sido eliminado', 'success');
        
        }).catch((error)=>{
          swal('No es posible eliminar el libro.','','error')
        })
    }

  },created(){
    this.getBook();
  },
}
</script>

<style lang="css" scoped>

</style>
