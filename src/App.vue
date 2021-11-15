<template>
  <div id="app">
    <header>
      <center> <h1>La Musica</h1> </center>
    </header>
    <div>
        <p> {{ current.title }} <br /> {{ current.artist }} </p>
    </div>
    <div class="btns_controle">
      <button class="prev" @click="prev">Previous</button>
      <button class="play" v-if="!isPlaying" @click="play">Play</button>
      <button class="pause" v-else @click="pause">Pause</button>
      <button class="next" @click="next">Next</button>
    </div>

    <div class="playlist">
      <button v-for="song in songs" :key="song.src" @click="play(song)" >
        {{ song.title }} | {{song.artist }}
      </button>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      songs : [
      {
        title : "caves of dawn",
        artist : "caves",
        src : require("./assets/caves-of-dawn-10376.mp3")
      },
      {
        title : "Monplaisir brotherhood",
        artist : "monplaisir",
        src : require("./assets/Monplaisir_-_15_-_Brotherhood.mp3")
      },
      {
        title : "sb_indreams",
        artist : "noka",
        src : require("./assets/sb_indreams.mp3")
      },
      {
        title : "warm memories emotional inspiration piano",
        artist : "montier",
        src : require("./assets/Warm-Memories-Emotional-Inspiring-Piano.mp3")
      },
    ],
    index : 0,
    current : {},
    player : new Audio(),
    isPlaying:false
    }
  },
  methods:{
    play(song){
      if( typeof song.src != "undefined" ){
        this.current = song;
        this.player.src  = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    next(){
      this.index++;
      if(this.index > this.songs.length -1 ){
        this.index=0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev(){
      this.index--;
      if(this.index < 0 ){
        this.index=this.songs.length-1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);

    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play();
  }
}
</script>

<style >
.btns_controle {
    text-align: center;
}
button.prev {
    font-size: 31px;
    text-align: center;
    background: #ecf0f1;
    border: none;
    color: #e74c3c;
}
button.play {
    font-size: 49px;
    text-align: center;
    background: #ecf0f1;
    border: none;
    padding: 20px;
    color: #e74c3c;
    margin: 10px;
}
button.next {
    font-size: 31px;
    text-align: center;
    background: #ecf0f1;
    border: none;
    color: #e74c3c;
}
.playlist {
    display: block;
    margin: 20px;
    text-align: center;
    border: none;
    color: #e74c3c;
}
header {
    background: #ecf0f1;
    margin: 0px!important;
    padding: 0px!important;
    color: #e74c3c;
    font-size: 29px;
}
p {
    text-align: center;
    color: #e74c3c;
    font-size: 39px;
}
body {
    background: #34495e;
}
</style>
