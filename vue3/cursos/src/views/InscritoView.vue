<template>
  <div>
  <Tabs>
    <template v-slot:lista>
      <h4>LISTA DE REGISTROS DE INSCRITOS</h4>
      <table class="highlight" style="background-color: darkgrey; text-align: center;">
        <thead style="background-color:lightblue;">
          <tr style="background-color:lightblue; color:white;">
             <th>Curso</th>
             <th>Tipo del curso</th>
             <th>materia</th>
              <th>Nombre del Estudiante</th>
              <th>Apellido Paterno del estudiante</th>
              <th>Apellido Materno del estudiante</th>
              <th>semestre</th>
              <th>tipo</th>
              <th>año</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="inscrito in items">
            <td>{{ inscrito.curso }}</td>
            <td>{{ inscrito.tipo }}</td>
            <td>{{ inscrito.materia }}</td>
            <template v-for="(estudiantereg,index) in inscrito.Estudiantes" :key="estudiantereg.id">
              <td v-if="index=='nombres'">{{estudiantereg}}</td>
              <td v-if="index=='apellido_paterno'">{{estudiantereg}}</td>
              <td v-if="index=='apellido_materno'">{{estudiantereg}}</td>
            </template>
            <template v-for="(gestionreg,index) in inscrito.Gestions" :key="gestionreg.id">
              <td v-if="index=='numero'">{{gestionreg}}</td>
              <td v-if="index=='tipo'">{{gestionreg}}</td>
              <td v-if="index=='anio'">{{gestionreg}}</td>
            </template>
          </tr>
        </tbody>
      </table>
    </template>
    <template v-slot:nuevo>
  <div class="row">
    <form class="col s12" @submit.prevent="saveInscrito()">
      <div class="row">
        <div class="input-field col s12">
    <select v-model="payload.EstudiantesId">
      <option value="" disabled selected>Seleccione carnet de identidad del estudiante</option>
      <template v-for="est in itemtodoslosest">
      <option :value="est.id">{{ est.cedulaidentidad }}</option>
    </template>
    </select>
    <label>Seleccione el estudiante</label>
      </div>
    </div>
      <div class="row">
        <div class="input-field col s4">
        <select v-model="payload.GestionsId">
      <option value="" disabled selected>Seleccione Gestion</option>
      <template v-for="gestionselect in itemtodosgestion">
      <option :value="gestionselect.id" v-if="gestionselect.numero!=0">{{ gestionselect.tipo}}-{{ gestionselect.numero }}-{{ gestionselect.anio }}</option>
      <option :value="gestionselect.id" v-else>{{ gestionselect.tipo}}-{{ gestionselect.anio }}</option>
      </template>
      </select>
      <label>Seleccione Gestion</label>
      </div>
          <div class="input-field col s4">
          <input id="curso" type="text" class="validate" v-model="payload.curso">
          <label for="curso">Curso</label>
         </div>
         <div class="input-field col s4">
    <select v-model="payload.tipo">
      <option value="" disabled selected>Tipo de Materia</option>
      <option value="optativa">optativa</option>
      <option value="principal">principal</option>
    </select>
    <label>Tipo de Materia</label>
  </div>
    </div>
    <div class="row">
        <div class="input-field col s12">
          <input id="materia" type="text" class="validate" v-model="payload.materia">
          <label for="materia">Materia</label>
        </div>
      </div>
        <div class="row">
        <div class="col s12">
        <button class="btn waves-effect waves-light" type="submit" name="action">Inscribir
         <i class="material-icons right">save</i>
        </button>
      </div>
    </div>
    </form>
  </div>
    </template>
  </Tabs>
  <pre>{{ payload }}</pre>
  </div>
</template>

<script>
// @ is an alias to /src
import Tabs from '@/components/Tabs.vue';
const api=process.env.VUE_APP_API;
export default {
  name: 'Inscrito',
  data(){
    return{
       items:[],
       itemsest:[],
       itemgestion:[],
       itemtodoslosest:[],
       itemtodosgestion:[],
       api,
       payload:{
        EstudiantesId: '',
        GestionsId: '',
        curso: '',
        tipo: '',
        materia: '',       
      },
       idDel:0
    }
  },
  methods: {
    getobtenerdatostodosestudiante()
    {
      this.axios({
                method: 'get',
                url: this.api + '/Estudiantes/'
            })
                .then((response) => {
                    this.itemtodoslosest = response.data;
                    console.log(response);
                    setTimeout(function () {
                        var elems = document.querySelectorAll('select');
                        var select = M.FormSelect.init(elems);
                    });
                })
                .catch((error) => { console.log(error) })
                .finally(() => { }); 
    },
    getobtenerdatostodosgestion()
    {
      this.axios({
                method: 'get',
                url: this.api + '/Gestions/'
            })
                .then((response) => {
                    this.itemtodosgestion = response.data;
                    console.log(response);
                    setTimeout(function () {
                        var elems = document.querySelectorAll('select');
                        var select = M.FormSelect.init(elems);
                    });
                })
                .catch((error) => { console.log(error) })
                .finally(() => { }); 
    },
    getobtenerdatosestudiante(id)
    {
      this.axios({
                method: 'get',
                url: this.api + '/Gestions/'+id
            })
                .then((response) => {
                    this.itemest = response.data;
                    console.log(response);
                    setTimeout(function () {
                        var elems = document.querySelectorAll('select');
                        var select = M.FormSelect.init(elems);
                    });
                })
                .catch((error) => { console.log(error) })
                .finally(() => { }); 
    },
    getInscritos(){
      this.axios({
                method: 'get',
                url: this.api + '/Gestion_Estudiantes?_expand=Gestions&_expand=Estudiantes'
            })
                .then((response) => {
                    this.items = response.data;
                    console.log(response);
                    setTimeout(function () {
                        var elems = document.querySelectorAll('select');
                        var select = M.FormSelect.init(elems);
                    });
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
    },
    saveInscrito(){
      this.axios({
                method: 'post',
                url: this.api + '/Gestion_Estudiantes',
                data:this.payload
            })
                .then((response) => {
                    this.payload = {
                      EstudiantesId: '',
                      GestionsId: '',
                      curso: '',
                      tipo: '',
                      materia: '',             
                    }
                    this.getInscritos();
                    console.log(response);
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
    },
    eliminarGestion(id){
        this.axios({
          method:'delete',
          url:this.api+'/Gestions/'+id
        }).then((response)=>{
            this.getGestiones();
            console.log(response);
        });
    },
    togglepopup(id){
      this.popupval=!this.popupval;
      this.idDel=id;
      //console.log(id);
    }
  },
  components: {
    Tabs
  },
  mounted(){
    this.getInscritos();
    this.getobtenerdatostodosestudiante();
    this.getobtenerdatostodosgestion();
  },
  created(){
    setTimeout(function () {
      var elems = document.querySelectorAll('select');
      var select = M.FormSelect.init(elems);
   });
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
