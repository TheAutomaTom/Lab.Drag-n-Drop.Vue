<style scoped>

  .game-board{
    position: absolute;
    width:80vw;
    height:80vw;
    height:80vw;
    overflow:hidden;

    background-color: blue;
    display: grid;
    grid-template-rows: 1fr 1fr 1fr 1fr 1fr;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;

  }

  .game-square{
    display: flex;
  align-items: center;
  justify-content: center;
  }

  .game-square-i{
    background-color: red;

  }

  .game-square-o{
    background-color: darkslategrey;
  }

  .a1{ grid-row:1; grid-column:1; }
  .a2{ grid-row:1; grid-column:2; }
  .a3{ grid-row:1; grid-column:3; }
  .a4{ grid-row:1; grid-column:4; }
  .a5{ grid-row:1; grid-column:5; }
  
  .b1{ grid-row:2; grid-column:1; }
  .b2{ grid-row:2; grid-column:2; }
  .b3{ grid-row:2; grid-column:3; }
  .b4{ grid-row:2; grid-column:4; }
  .b5{ grid-row:2; grid-column:5; }

  .c1{ grid-row:3; grid-column:1; }
  .c2{ grid-row:3; grid-column:2; }
  .c3{ grid-row:3; grid-column:3; }
  .c4{ grid-row:3; grid-column:4; }
  .c5{ grid-row:3; grid-column:5; }
  

</style>

<template>
  <div
    class="game-board"
  >
  <!-- a -->
  <div class="a1 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)">
    <img 
      id="drag1" 
      src="../../public/img_logo.gif"
      draggable="true" 
      @dragstart="dragStart($event)"
      width="50" 
      height="50"
      style="cursor: grab;"
    /> 
  </div>
  <div class="a2 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  <div class="a3 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  <div class="a4 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  <div class="a5 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  
  <!-- b -->
  <div class="b1 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="b2 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="b3 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="b4 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="b5 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>

  <!-- c -->
  <div class="c1 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="c2 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="c3 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="c4 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div class="c5 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>

  <img 
    id="drag3" 
    src="../../public/img_logo3.gif"
    draggable="true" 
    @dragstart="dragStart($event)"
    width="50" 
    height="50"
    style="cursor: grab;"
  /> 
  
  <img 
    id="drag2" 
    src="../../public/img_logo2.gif"
    draggable="true" 
    @dragstart="dragStart($event)"
    width="50" 
    height="50"
    style="cursor: grab;"
  /> 


  </div>
</template>

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

