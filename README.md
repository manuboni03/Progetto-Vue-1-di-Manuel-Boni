#***Progetto Vue 1 di Manuel Boni***

Questo è il mio progetto tramite uno dei framework di *Javascript*, **Vue Js**, del famoso gioco *Tic Tac Toe*

## Introduttiva 

___ 

il gioco si sviluppa tramite click sullo schermo dov'è rappresentata la griglia, tra l'utente e la CPU, rispettivsamente la X e la O

per svilupparlo mi sono servito di questi linguaggi:
- **HTML**
- **Javascript**
- **CSS**

questi tre formano solo il contorno dell'app; il vero codice sorgente è stato realizzato con [Vue Js](https://it.vuejs.org/)

## Come funziona 

___

All'interno del file *index.html* nel body troviamo solo lo script che rimanda ad un altro file, *main.js* il quale ha al suo interno il necessario per importare codice dal file *app.vue*, ovvero: 
```Javascript
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```
Questo serve a trasferire nel file Javascript tutto ciò che è presente nel file Vue. 
All'interno del file Vue invece troviamo:
-una parte **HTML** rappresentata dal *<template>*
-una parte **CSS** rappresentata da *<style scoped>*
-una parte **Javascript** rappresentata da *<script setup>* 

La parte **HTML** è formata da un *div contenitore* con al suo interno altri 9 *div* con al loro interno il contenuto dinamico che dovrà variare tra X o O. 
Nella parte dello script invece viene creato un oggetto dinamico (che sarà quello all'interno dei *div*) grazie alle funzionalità di **Vue**: 
```Javascript
import {ref, reactive} from 'vue'

let segnoTurno = ref('X');
let turno = ref(1);
let griglia = reactive({});

for (let i=0; i<9; i++){
  griglia.key = i;
  griglia.value = ref('');
  console.log(`${griglia.key}: ${griglia.value}`);
}
```

Subito dopo è presente un *listener di eventi*, ***on-click***, il quale tiene conto del turno (se dispari gioca X e viceversa) ed elabora anche la risposta della CPU. 
A questo evento sono collegate 3 funzioni: 
1) Controllo se un giocatore ha vinto (ciclo *While* con diversi *if* al suo interno che verificano tutte le combinazioni)
2) Una funzione che stampa a video il vincitore
3) Una funzione che riaggiorna la pagina dopo tot tempo dalla vittoria (per rigiocare)

***per controllare meglio verifica il codice sorgente app.vue in questa repository***

## Uso

L'uso di quest'app è molto semplice se sai le regole del gioco. In pratica ti basta cliccare le caselle e vincere

## Contatto 

___


Per qualsiasi problema, chiarimento o informazioni puoi contattarmi qui:

- La mia pagina web:
[Vai alla mia pagina](https://manuboni03.github.io/Progetto-HTML-e-CSS-di-Manuel-Boni/sito.html)

- Il mio indirizzo email:
manuelboni2904@gmail.com

Per dare un'occhiata ai miei progetti visita il mio profilo Git:
[Github](https://github.com/manuboni03)

