<template>
  <h4>Editar Cliente</h4>
  <div class="row">
    <form class="col s12" @submit.prevent="saveEstudiante()">
      <div class="row">
        <div class="input-field col s6">
          <input id="carnetid" type="text" class="validate" v-model="payload.cedulaidentidad">
          <label for="carnetid">Cedula de Identidad</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s6">
          <input id="nombres" type="text" class="validate" v-model="payload.nombres">
          <label for="nombres">Registre sus Nombres</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input id="apellidop" type="text" class="validate" v-model="payload.apellido_paterno">
          <label for="apellidop">Apellido Paterno</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input id="apellidom" type="text" class="validate" v-model="payload.apellido_materno">
          <label for="apellidom">Apellido Materno</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input id="direccion" type="text" class="validate" v-model="payload.direccion">
          <label for="direccion">Direccion</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s6">
          <input id="zona" type="text" class="validate" v-model="payload.zona">
          <label for="zona">Zona</label>
        </div>
        <div class="input-field col s6">
          <input id="phone" type="text" class="validate" v-model="payload.phone">
          <label for="phone">Telefono</label>
        </div>
        <div class="row">
        <div class="col s6">
        <button class="btn waves-effect waves-light" type="submit" name="action">Guardar
         <i class="material-icons right">save</i>
        </button>
      </div>
    </div>
      </div>
    </form>
  </div>
</template>

<script>
// @ is an alias to /src
import Tabs from '@/components/Tabs.vue';
import Popup from '@/components/PopupEstudiante.vue';
const api=process.env.VUE_APP_API;
export default {
  name: 'Estudiante',
  data(){
    return{
       api,
       payload:{
        cedulaidentidad:'',
        nombres:'',
        apellido_paterno:'',
        apellido_materno:'',
        direccion:'',
        zona:'',
        phone:''
       },
    }
  },
  methods: {
    saveEstudiante(){
      this.axios({
                method: 'put',
                url: this.api + '/Estudiante/',
                data:this.payload
            })
                .then((response) => {
                    this.payload = {
                      cedulaidentidad:'',
                      nombres:'',
                      apellido_paterno:'',
                      apellido_materno:'',
                      direccion:'',
                      zona:'',
                      phone:''      
                    }
                    console.log(response);
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
    },
    getEstudiante(){
      this.axios({
         method: 'get',
         url: this.api + '/Estudiante/'+this.$route.params.id
      })
      .then((response) => {
        this.payload = response.data;
        setTimeout(function () {
          M.updateTextFields();
        });
        console.log(response);
      })
      .catch((error) => { console.log(error) })
       .finally(() => { });
    }
  },
  components: {
  },
  created(){
    this.getEstudiante();
  }
}
</script>
<style scoped lang="scss">
  .color-box {
                width: 40px;
                height: 40px;
                border-radius: 50%;
                margin: 7px;
                display: inline-block;
            }

            .clic,.elimina{
                cursor: pointer;
            }

            .quantity button{
                border-radius: 50%;
                display: inline-block;
                width: 30px;
            }
            .quantity div{
                text-align: center;
                min-width: 30px;
                display: inline-block;
                font-weight: bold;
            }
            .buy-box{
                margin: 20px;
            }
            footer {
                
                text-align: center;
                padding: 30px 10px;
                margin-top: 50px;
                min-height: 100px;
            }
            .container{
                margin-top: 50px;
            }
            .producto-relacionado-precio{
                background: orangered;
                color: white;
                text-align: center;
                padding: 10px; 
            }
            .contenido{
              background: orangered;
            }
  </style>