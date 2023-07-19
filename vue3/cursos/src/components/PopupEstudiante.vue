<template>
    <div class="popup">
     <div class="popup-inner">
       <slot></slot>
       <button class="popup-delete btn waves-effect waves-light" @click="$emit('eliminarest')"> Aceptar </button>
       <button class="popup-close btn waves-effect waves-light" @click="$emit('togglepopup')"> Cancelar </button> 
    </div>
    </div>
  </template>
  
  <script>

  export default {
    name: 'Popup',
    props: ['popupval','val'],
    emits:['togglepopup','eliminarest'],
    data(){
    return{
    }
   },
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped lang="scss">
   .popup{
    position: fixed;
    top: 0;
    left:0;
    right: 0;
    bottom: 0;
    z-index: 99;
    background-color: rgba(217, 235, 235, 0.518);
    display: flex;
    align-items: flex;
    align-items: center;
    justify-content: center;
   }
   .popup-inner{
    background:lightblue;
    padding: 32px;
   }
   .popup button{
    margin-left: 10px;
    margin-right: 10px;
   }
  </style>
  