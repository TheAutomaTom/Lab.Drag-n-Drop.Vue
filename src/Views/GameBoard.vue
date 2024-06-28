
<style scoped>

  table{
    color:white;
    width:100%;
    border:1px solid white;
    text-wrap:nowrap;
  }

  table td{
    width:100%;
    text-wrap:nowrap;
  }

  .game-board{
    position: absolute;
    overflow:hidden;

    background-color: blue;
    display: grid;
    grid-template-rows: 9em 9em 9em 9em 9em;
    grid-template-columns: 9em 9em 9em 9em 9em;

  }

  .game-square{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .game-square-i{ background-color: red; }
  .game-square-o{ background-color: darkslategrey; }

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
  
  .game-piece{
    width:100%;
    height:100%;
    object-fit:scale-down;
    cursor: grab;
    
  }

</style>

<template>
  <div
    class="game-board"
  >
  <!-- a -->
  <div id="a1" class="a1 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)">
    <img 
    id="piece-1" 
    src="../../public/piece-1.png"
      draggable="true" 
      @dragstart="dragStart($event)"
      class="game-piece"
    /> 
  </div>
  <div id="a2" class="a2 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  <div id="a3" class="a3 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  <div id="a4" class="a4 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  <div id="a5" class="a5 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)" ></div>
  
  <!-- b -->
  <div id="b1" class="b1 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div id="b2" class="b2 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div id="b3" class="b3 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div id="b4" class="b4 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)">
    <img 
    id="piece-2" 
    src="../../public/piece-2.png"
      draggable="true" 
      @dragstart="dragStart($event)"
      class="game-piece"
    /> 
  </div>
  <div id="b5" class="b5 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>

  <!-- c -->
  <div id="c1" class="c1 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div id="c2" class="c2 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)">
    <img 
    id="piece-3" 
    src="../../public/piece-3.png"
      draggable="true" 
      @dragstart="dragStart($event)"
      class="game-piece"
    /> 
  </div>
  <div id="c3" class="c3 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div id="c4" class="c4 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)"></div>
  <div id="c5" class="c5 game-square game-square-i" @drop="drop($event)" @dragover="dragOver($event)"></div>

<!-- Info -->
<table>
  <tr>
    <td>Object Id:</td>
    <td>{{ object }}</td>
  </tr>
  <tr>
    <td>Start:</td>
    <td>{{ start }}</td>
  </tr>
  <tr>
    <td>Over:</td>
    <td>{{ over }}</td>
  </tr>
  <tr>
    <td>Drop:</td>
    <td>{{ dropped }}</td>
  </tr>
</table>



</div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

  const object = ref("");
  const start = ref("");
  const over = ref("");
  const dropped = ref("");

  const dragOver = (ev: any) => {
    over.value = (((((ev as DragEvent).target) as HTMLElement).id) );

    ev.preventDefault();
  }
  

  const dragStart = (ev: any) => {
    object.value = (((ev as DragEvent).target) as HTMLElement).id;
    ev.dataTransfer.setData("text", ev.target.id);
    
    start.value = (((((ev as DragEvent).target) as HTMLElement).parentElement) as HTMLElement).id;
  }

  const drop = (ev: any) => {
    ev.preventDefault();
    var data = ev.dataTransfer.getData("text");
    ev.target.appendChild(document.getElementById(data));
    
    dropped.value = (((ev as DragEvent).target) as HTMLElement).id;

  } 


</script>




