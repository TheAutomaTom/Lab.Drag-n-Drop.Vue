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
  <div id="a2" class="a2 game-square game-square-o" @drop="drop($event)" @dragover="dragOver($event)" >
    <div 
      id="piece-4" 
      draggable="true" 
      @dragstart="dragStart($event)"
      class="game-piece"
      style="display:flex;align-items: center; justify-content: center;"
    > <span>What a Drag.</span>
    </div>
  </div>
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
    <td>Piece:</td>
    <td>{{ trackedPiece }}</td>
  </tr>
  <tr>
    <td>Start:</td>
    <td>{{ trackedStart }}</td>
  </tr>
  <tr>
    <td>Over:</td>
    <td>{{ trackedOver }}</td>
  </tr>
  <tr>
    <td>Drop:</td>
    <td>{{ trackedDrop }}</td>
  </tr>
</table>

</div>
</template>

<script setup lang="ts">
  import { computed, ref } from 'vue';

  const trackedPiece = ref("");
  const trackedStart = ref("");
  const trackedOver = ref("");
  const trackedDrop = ref("");


  // const getGamePieceClass = (piece: string): string => {
  //   if(piece == trackedDrop.value){
    
  //     if(trackedOver.value.includes("piece-")){
  //       console.log("game-piece-no-drop")
  //       return "game-piece-no-drop";
  //     }
  //     console.log("game-piece-dragging")
  //     return "game-piece-dragging";
  //   }
  //   console.log("game-piece-grab")
  //   return "game-piece-grab";
  // };

  // const getGamePieceClass = computed((piece: string): string => {
  //   if(piece == trackedDrop.value){
    
  //     if(trackedOver.value.includes("piece-")){
  //       console.log("game-piece-no-drop")
  //       return "game-piece-no-drop";
  //     }
  //     console.log("game-piece-dragging")
  //     return "game-piece-dragging";
  //   }
  //   console.log("game-piece-grab")
  //   return "game-piece-grab";
  // });



  const dragOver = (ev: any) => {
    trackedOver.value = (((((ev as DragEvent).target) as HTMLElement).id) );
    ev.preventDefault();
  }; 

  const dragStart = (ev: any) => {
    trackedPiece.value = (((ev as DragEvent).target) as HTMLElement).id;
    ev.dataTransfer.setData("text", ev.target.id);
    
    trackedStart.value = (((((ev as DragEvent).target) as HTMLElement).parentElement) as HTMLElement).id;
  }

  const drop = (ev: any) => {
    ev.preventDefault();
    var data = ev.dataTransfer.getData("text");
    ev.target.appendChild(document.getElementById(data));    
    trackedDrop.value = (((ev as DragEvent).target) as HTMLElement).id;
  } 


</script>

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
    z-index:100;
    width:100%;
    height:100%;
    object-fit:scale-down;
    cursor:grab;
  }
  .game-piece:active{
    cursor: grabbing;
  }
  /* .game-piece-grab{
    cursor:grab !important;
  }
  
  .game-piece-no-drop{
    cursor:no-drop !important;
  }
  
  .game-piece-dragging{
    cursor: grabbing !important;
  } */

</style>
