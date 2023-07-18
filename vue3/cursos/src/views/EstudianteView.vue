<template>
  <div>
  <Tabs>
    <template v-slot:lista>
      <h4>LISTA DE REGISTROS DE ESTUDIANTES</h4>
      <table class="highlight" style="background-color: darkgrey;">
        <thead style="background-color:lightblue;">
          <tr style="background-color:lightblue; color:white;">
              <th>Cedula de Identidad</th>
              <th>Nombres</th>
              <th>Apellido Paterno</th>
              <th>Apellido Materno</th>
              <th>Direccion</th>
              <th>Zona</th>
              <th>Telefono</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="estudiante in items">
            <td>{{ estudiante.cedulaidentidad }}</td>
            <td>{{ estudiante.nombres }}</td>
            <td>{{ estudiante.apellido_paterno }}</td>
            <td>{{ estudiante.apellido_materno }}</td>
            <td>{{ estudiante.direccion }}</td>
            <td>{{ estudiante.zona }}</td>
            <td>{{ estudiante.phone }}</td>
          </tr>
        </tbody>
      </table>
    </template>
    <template v-slot:nuevo>
      
  <div class="row">
    <form class="col s12">
      <div class="row">
        <div class="input-field col s6">
          <input id="carnetid" type="text" class="validate">
          <label for="carnetid">Cedula de Identidad</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s6">
          <input id="nombres" type="text" class="validate">
          <label for="nombres">Registre sus Nombres</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input id="apellidop" type="text" class="validate">
          <label for="apellidop">Apellido Paterno</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input id="apellidom" type="text" class="validate">
          <label for="apellidom">Apellido Materno</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input id="direccion" type="text" class="validate">
          <label for="direccion">Direccion</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s6">
          <input id="zona" type="text" class="validate">
          <label for="zona">Zona</label>
        </div>
        <div class="input-field col s6">
          <input id="phone" type="text" class="validate">
          <label for="phone">Telefono</label>
        </div>
        <div class="row">
        <div class="col s6">
        <button class="btn waves-effect waves-light" type="submit" name="action">Submit
         <i class="material-icons right">save</i>
        </button>
      </div>
    </div>
      </div>
    </form>
  </div>
    </template>
  </Tabs>
  </div>
</template>

<script>
// @ is an alias to /src
import Tabs from '@/components/Tabs.vue'
const api=process.env.VUE_APP_API;
export default {
  
  name: 'Estudiante',
  data(){
    return{
       items:[],
       api
    }
  },
  methods: {
    getEstudiantes(){
      this.axios({
                method: 'get',
                url: this.api + '/Estudiante'
            })
                .then((response) => {
                    this.items = response.data;
                    console.log(response);
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
    }
  },
  components: {
    Tabs
  },
  mounted(){
    this.getEstudiantes();
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

            .clic{
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