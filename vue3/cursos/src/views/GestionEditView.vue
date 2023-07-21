<template>
  <h4>Editar Gestion</h4>
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
<script>
// @ is an alias to /src
const api=process.env.VUE_APP_API;
export default {
  name: 'GestionEdit',
  data(){
    return{
       api,
       payload:{
        tipo:'',
        numero:'',
        anio:''
       },
    }
  },
  methods: {
    saveGestiones(){
      this.axios({
                method: 'patch',
                url: this.api + '/Gestions/'+this.$route.params.id,
                data:this.payload
            })
                .then((response) => {
                    this.payload={
                    tipo:'',
                    numero:'',
                     anio:''
                   },
                    console.log(response);
                    window.location.href="../Gestion";
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
    },
    getGestion(){
      this.axios({
         method: 'get',
         url: this.api + '/Gestions/'+this.$route.params.id
      })
      .then((response) => {
        this.payload = response.data;
        setTimeout(function () {
          M.updateTextFields();
          var elems = document.querySelectorAll('select');
          var select = M.FormSelect.init(elems);
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
    this.getGestion();
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