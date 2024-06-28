<script setup lang="ts">

const dragOver = (ev: any) => {
  console.log(`allowDrop(${ev})`);
  ev.preventDefault();
}

const dragStart = (ev: any) => {
  console.log(`drag(${ev})`);
  ev.dataTransfer.setData("text", ev.target.id);
}

const drop = (ev: any) => {
  console.log(`drop(${ev})`);
  ev.preventDefault();
  var data = ev.dataTransfer.getData("text");
  ev.target.appendChild(document.getElementById(data));
}


</script>

<template>

  <div 
  id="div1" 
    @drop="drop($event)" 
    @dragover="dragOver($event)"
    style="border:2px solid grey;width:150px;height:150px;margin-bottom:15px"
  ></div>

  <div 
    id="div2" 
    @drop="drop($event)" 
    @dragover="dragOver($event)"
    style="border:2px solid grey;width:150px;height:150px;"
  ></div>

  <img 
    id="drag1" 
    src="../../public/img_logo.gif"
    draggable="true" 
    @dragstart="dragStart($event)"
    width="150" 
    height="150"
    style="cursor: grab;"
  /> 

</template>

<style scoped>

</style>
