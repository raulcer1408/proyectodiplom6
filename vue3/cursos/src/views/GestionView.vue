<template>
  <div>
  <Tabs>
    <template v-slot:lista>
      <h4>LISTA DE REGISTROS DE GESTIONES</h4>
      <search placeholder="Buscar Gestion" @searchtext="searchFx($event)"></search>
      <FilterApp>
        <div class="input-field" style="display:inline-block">
            <input id="filtro" type="search" class="validate">
            <label for="filtro">filtro año</label>
          </div>
          <button class="popup-delete btn waves-effect waves-light" @click="onFilterFx()">Filtrar</button>
      </FilterApp>
      <table class="highlight" style="background-color: darkgrey; text-align: center;">
        <thead style="background-color:lightblue;">
          <tr style="background-color:lightblue; color:white;">
              <th>Tipo</th>
              <th>Numero de Semestre</th>
              <th>Año</th>
              <th>opciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="gestion in items">
            <td>{{ gestion.tipo }}</td>
            <td v-if="gestion.numero==0">Toda la gestion</td>
            <td v-if="gestion.numero!=0">{{ gestion.numero }}</td>
            <td>{{ gestion.anio }}</td>
            <td>
             <i class="elimina material-icons" style="color:red" @click="togglepopup(gestion.id)">
                delete_forever</i>
             <router-link :to="'/Gestion/'+gestion.id"><i class="material-icons">create</i></router-link>
            </td>
          </tr>
        </tbody>
      </table>
    </template>
    <template v-slot:nuevo>
  <div class="row">
    <form class="col s12" @submit.prevent="saveGestiones()">
      <div class="row">
        <div class="input-field col s4">
          <input id="tipo" type="text" class="validate" v-model="payload.tipo">
          <label for="tipo">Registro del tipo</label>
        </div>
        <div class="input-field col s4">
        <select v-model="payload.numero">
      <option value="" disabled selected>Elija una opcion</option>
      <option value="1">semestre 1</option>
      <option value="2">semestre 2</option>
      <option value="0">toda la gestion</option>
    </select>
    <label>Seleccione semestre o gestion</label>
  </div>
      </div>
      <div class="row">
        <div class="input-field col s4">
          <input id="anio" type="text" class="validate" v-model="payload.anio">
          <label for="anio">Año</label>
        </div>
      </div>
        <div class="row">
        <div class="col s6">
        <button class="btn waves-effect waves-light" type="submit" name="action">Guardar
         <i class="material-icons right">save</i>
        </button>
      </div>
    </div>
    </form>
  </div>
    </template>
  </Tabs>
  <PopupG :popupval=popupval :val=idDel v-if="popupval" @togglepopup="togglepopup('0')" @eliminargest="eliminarGestion(idDel)">
    <h6 style="color: white;">Esta seguro de eliminar la Gestion?</h6>
  </PopupG>
  <pre>{{ payload }}</pre>
  </div>
</template>

<script>
// @ is an alias to /src
import Tabs from '@/components/Tabs.vue';
import PopupG from '@/components/PopupDeleteGest.vue';
import search from '@/components/Search.vue';
import FilterApp from '@/components/filterGroup.vue';
import FilterItem from '@/components/Filteritem.vue';
const api=process.env.VUE_APP_API;
export default {
  name: 'Gestion',
  data(){
    return{
       items:[],
       api,
       payload:{
        tipo:'',
        numero:'',
        anio:'',
        tosearch:'',
        tofilter:''
       },
       popupval:false,
       idDel:0
    }
  },
  methods: {
    getGestiones(){
      this.axios({
                method: 'get',
                url: this.api + '/Gestions?'+this.tosearch
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
    getGestionesconfiltro(){
      this.axios({
                method: 'get',
                url: this.api + '/Gestions?'+this.tosearch+this.tofilter
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
    saveGestiones(){
      this.axios({
                method: 'post',
                url: this.api + '/Gestions',
                data:this.payload
            })
                .then((response) => {
                    this.payload = {
                      tipo:'',
                      numero:'',
                      anio:''             
                    }
                    this.getGestiones();
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
            this.togglepopup(0);
            console.log(response);
        });
    },
    togglepopup(id){
      this.popupval=!this.popupval;
      this.idDel=id;
      //console.log(id);
    },
    searchFx(event){
      if(event==''){
        this.tosearch='';
      }else{
        this.tosearch='&q='+event;
      }
      this.getGestiones();
    },
    onFilterFx() {
      let field='anio';
      let event=document.getElementById('filtro').value;
      if (event === '') {
        this.tofilter = '';
      } else {
        this.tofilter = '&' + field + '='+event;
      }
      this.getGestionesconfiltro();
    },
  },
  components: {
    Tabs,PopupG,search,FilterApp,FilterItem
  },
  mounted(){
    this.getGestiones();
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
