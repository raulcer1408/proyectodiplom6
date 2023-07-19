<template>
     <div class="row">
      <ul class="tabs">
          <li class="tab col s3">
            <a href="#listar">
              Listar
              <i class="tiny material-icons">view_list</i>    
          </a>  
          </li>
          <li class="tab col s3">
          <a href="#nuevo">Nuevo
            <i class=" tiny material-icons">add</i>
          </a>           
        </li>
        </ul>
      <div id="listar" class="col s12"><slot name="lista"></slot>
      
      </div>
      <div id="nuevo" class="col s12"><slot name="nuevo"></slot></div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Tabs',
    created() {
      setTimeout(() => {
        var elems = document.querySelectorAll('.tabs');
        var tabs = M.Tabs.init(elems);
      });
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped lang="scss">
  .tabs{
    position:inherit;
    background-color: white;
    color:lightblue;
    text-align: center;
  }
  .tabs .tab a:hover{
    background-color:lightblue/* put some background color*/;
    color:white/* put some font color*/;
  }
.tabs .tab a.active{
    background-color:white/* put some background color*/;
    color:lightblue/* put some font color*/;
}
.tabs .tab a {
  background-color: white;
  color: lightblue;
}
  .row{
    z-index: -1;
    position:static;
  }
  </style>