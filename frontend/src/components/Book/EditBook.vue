<template>
  <div class="containder">
    <div class="row">
      <div class="col text-left">
        <h2>Editar Libro</h2>
      </div>
    </div>
  <div class="row">
    <div class="col">
      <div class="card-body">
        <form @onSubmit ="onSubmit">

          <div class="form-group row">
              <label for="title" class="col-md-2 col-form-label">Titulo</label>
              <div class="col-sm-6">
                <input type="text" placeholder="Titulo" name="title" class="form-control" v-model.trim="form.title">
              </div>
          </div>

          <div class="form-group row">
              <label for="description" class="col-md-2 col-form-label">Descripción</label>
              <div class="col-sm-6">
                <textarea name="description" class="form-control" rows="3" placeholder="Descripsión" v-model.trim="form.description"></textarea>
              </div>
          </div>

            <div class="row">
              <div class="col text-left">
                <b-button size="sm" variant="primary">Editar</b-button>
                <b-button size="sm" class="btn-large-space" :to= "{ name: 'ListBook'}">Cancelar</b-button>
              </div>
            </div>
        </form>
      </div>
    </div>
  </div>
  </div>
 
</template>

<script>
import axios from "axios"

export default {

    data(){
      return{
        bookId: this.$route.params.bookId,
        form: {
          title: '',
          description: ''
        }
      }
    },
    methods:{
      onSubmit(evt){
        evt.preventDefault();
      },
      getBook(){
        const path =`http://localhost:8000/api/v1.0/books/${this.bookId}/`
        axios.get(path).then((responser)=>{
          this.form.title = responser.data.title;
          this.form.description = responser.data.description;
        }).catch((error)=>{
          console.log(error);
        })
      }
    },created(){
      this.getBook();
    }
    }


</script>