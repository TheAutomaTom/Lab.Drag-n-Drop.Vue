<script setup lang="ts">

function allowDrop(ev: any) {
  ev.preventDefault();
}

function drag(ev: any) {
  ev.dataTransfer.setData("text", ev.target.id);
}

function drop(ev: any) {
  ev.preventDefault();
  var data = ev.dataTransfer.getData("text");
  ev.target.appendChild(document.getElementById(data));
}
</script>

<template>

<div 
  id="div1" 
  ondrop="drop(event)" 
  ondragover="allowDrop(event)"
>[]</div>

<img 
  id="drag1" 
  src="../public/img_logo.gif"
  draggable="true" 
  ondragstart="drag(event)"
  width="70" 
  height="70"
/>  


</template>

<style scoped>

</style>
