<template>
  <div class="containder">
    <div class="row">
      <div class="col text-left">
        <h2>Nuevo Libro</h2>
      </div>
    </div>
  <div class="row">
    <div class="col">
      <div class="card-body">
        <form @submit ="onSubmit">

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
                <b-button size="sm" variant="primary" type="submit">Crear</b-button>
                <b-button size="sm" type="submit" class="btn-large-space" :to= "{ name: 'ListBook'}">Cancelar</b-button>
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
import swal from 'sweetalert';

export default {

    data(){
      return{

        form: {
          title: '',
          description: ''
        }
      }
    },
    methods:{
      onSubmit(evt){
        evt.preventDefault();
         const path =`http://localhost:8000/api/v1.0/books/`
        axios.post(path, this.form).then((responser)=>{
          this.form.title = responser.data.title;
          this.form.description = responser.data.description;
          swal("¡Libro creado exitosamente!" ,"", "success");
        }).catch((error)=>{
          swal("¡El Libro no ha sido creado!" ,"", "error");
        })
      }
    },created(){
      
    }
    }


</script>
