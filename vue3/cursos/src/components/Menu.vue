<template>
    <div>
        <nav class="navbar navbar-expand-lg " v-bind:style="'background-color:'+menuColor">
        <div class="container-fluid" v-bind:style="'background-color:'+menuColor">
                <img alt="Vue logo" src="../assets/home.png" width="40" height="40">        
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent" >
                <ul class="navbar-nav me-auto mb-2 mb-lg-0" >
                  <li><router-link to="/">Inicio</router-link></li>
                  <li><router-link to="/Gestion" >Gestion</router-link></li>
                  <li><router-link to="/Estudiante" >Estudiante</router-link></li>
                  <li><router-link to="/about">About</router-link></li> 
                </ul>
            </div>
        </div>
      </nav>
    </div>
    <slot></slot>
  </template>
  <script>
  export default {
    name:'Menu', 
    data(){
        return{
            menuColor: "lightblue",
        }
    },
    created(){
       
     }
    }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
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
  </style>