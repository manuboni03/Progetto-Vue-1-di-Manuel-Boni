<script setup>
import {ref, reactive} from 'vue'

let segnoTurno = ref('X');
let turno = ref(1);
let griglia = reactive({});

for (let i=0; i<9; i++){
  griglia.key = i;
  griglia.value = ref('');
  console.log(`${griglia.key}: ${griglia.value}`);
}

function mettiSegno(numCella){
  if (griglia[numCella] != 'X' && griglia[numCella] != 'O'){
    if (turno.value%2!=0){
      griglia[numCella] = 'X';
      console.log(`${numCella}: X`);
      turno.value++;
      segnoTurno.value = 'O';

      if (turno.value < 9){
        let sceltaStr;
        let sceltaNum;
        do{
          sceltaStr = Math.random();
          sceltaStr = sceltaStr + '0';
          sceltaNum = Number(sceltaStr.slice(2,3));
        }while(sceltaNum > 8 || griglia[sceltaNum] === 'X' || griglia[sceltaNum] === 'O')

        setTimeout (function(){
          griglia[sceltaNum] = 'O';
          turno.value++;
          controllo('O');
          segnoTurno.value = 'X';
        }, 1000);

        controllo('X');
      }
    }
  }
  else {
    alert('spazio già occupato');
  }
}

function controllo(segno){
  let x=0, y=0;
  while (x<7 && y<3){
    if (griglia[x] == griglia[x+1] && griglia[x+1] == griglia[x+2]){
      if (griglia[x+1] === segno){
        giocaAncora(segno);
      }
    }
    
    if (griglia[y] == griglia[y+3] && griglia[y+3] == griglia[y+6]){
      if (griglia[y+3] === segno){
        giocaAncora(segno);
      }
    }

    if (griglia[0] == griglia[4] && griglia[4] == griglia[8]){
      if (griglia[4] === segno){
        giocaAncora(segno);
      }
    }

    if (griglia[2] == griglia[4] && griglia[4] == griglia[6]){
      if (griglia[4] === segno){
        giocaAncora(segno);
      }
    }
    y++;
    x = x+3;
  }
}

function giocaAncora(segnoVincente){
  let h2 = document.querySelector('h2');
  h2.innerHTML = 'Il vincitore è ' + segnoVincente ;
  setTimeout(function(){ window.location.reload();}, 2000);
}

function buttonGiocaAncora(){
  window.location.reload();
}
</script>

<template>
  <h1>Tic Tac Toe</h1>
  <p>Turno n°{{ turno }}, Tocca a: {{ segnoTurno }}</p>
  <div id="container">
    <div id="board">
      <div @click.prevent="mettiSegno(0)" data-index="1" class="tile right-border bottom-border">{{ griglia[0] }}</div>
      <div @click.prevent="mettiSegno(1)" data-index="2" class="tile right-border bottom-border">{{ griglia[1] }}</div>
      <div @click.prevent="mettiSegno(2)" data-index="3" class="tile bottom-border">{{ griglia[2] }}</div>
      <div @click.prevent="mettiSegno(3)" data-index="4" class="tile right-border bottom-border">{{ griglia[3] }}</div>
      <div @click.prevent="mettiSegno(4)" data-index="5" class="tile right-border bottom-border">{{ griglia[4] }}</div>
      <div @click.prevent="mettiSegno(5)" data-index="6" class="tile bottom-border">{{ griglia[5] }}</div>
      <div @click.prevent="mettiSegno(6)" data-index="7" class="tile right-border">{{ griglia[6] }}</div>
      <div @click.prevent="mettiSegno(7)" data-index="8" class="tile right-border">{{ griglia[7] }}</div>
      <div @click.prevent="mettiSegno(8)" data-index="9" class="tile">{{ griglia[8] }}</div>

      <div id="strike" class="strike"></div>
    </div>
    <div class="game-over-area">
      <h2 class="game-over-text"></h2>
      <button @click="buttonGiocaAncora()">Ricomincia</button>
    </div>
  </div>

</template>

<style scoped>
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
body{
    display: flex;
    flex-direction: column;
    align-items: center;
}
h1{
  text-align: center;
  font-size: 40px;
  color: red;
  padding-bottom: 20px;
}
h2{
    font-size: 2em;
    margin-top: 0px;
}
p{
  text-align: center;
  font-size: 30px;
  padding-bottom: 30px;
}
button{
    background-color: transparent;
    border: 1px solid indigo;
    padding: 10px;
    font-size: 1.5em;
}
button:focus{
  transform: scale(0.90);
  background-color: aquamarine;
}
button:hover{
  background-color: aquamarine;
}
#container{
  position: relative;
  left: 39%;
}
#board{
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
    cursor: pointer;
    position: relative;
    top: 4%;
}
.game-over-area{
    text-align: center;
    border: 8px solid indigo;
    margin: 30px;
    width: 20%;
    padding: 20px;
    position: relative;
    right: 1%;
}
.game-over-text{
  padding-bottom: 15px;
}
.tile{
    font-size: 2em;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
}
.right-border{
    border-right: 0.2em solid indigo;
}
.bottom-border{
    border-bottom: 0.2em solid indigo;
}
.strike{
    position: absolute;
    background-color: red;
}
.strike-row-1{
    width: 100%;
    height: 4px;
    top: 15%;
}
.strike-row-2{
    width: 100%;
    height: 4px;
    top: 48%;
}
.strike-row-3{
    width: 100%;
    height: 4px;
    top: 83%;
}
.strike-column-1{
    height: 100%;
    width: 4px;
    left: 15%;
}
.strike-column-2{
    height: 100%;
    width: 4px;
    left: 48%;
}
.strike-column-3{
    height: 100%;
    width: 4px;
    left: 83%;
}
.strike-diagonal-1{
    width: 90%;
    height: 4px;
    top: 50%;
    left: 5%;
    transform: skewY(45deg);
}
</style>
