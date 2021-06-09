<template>
  <div id="app">
    <header>
      <h1>Lofi Xmas Everly Mix</h1>
    </header>
    <main>
      <section>
        <h2 class="song-title">{{current.title}}</h2>
        <h3>{{current.artist}}</h3>
        <div class="controls">
          <button id="prev">Prev</button>
          <button id="playPause" v-if="!isPlaying">Play</button>
          <button id="playPause" v-else>Pause</button>
          <button id="next">Next</button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  //set states for current song and an array for all available songs
  data () {
    return{
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Deck The Halls',
          artist: 'Megan Wooffard',
          src: require('./assets/deck-the-halls_megan-wooffard.mp3')
        },
        {
          title: 'Jingle Bells',
          artist: 'Jobii',
          src: require('./assets/jingle-bells_jobii.mp3')
        },
        {
          title: 'Joy to the World',
          artist: 'Timothy Infinite',
          src: require('./assets/joy-to-the-world_timothy-infinite.mp3')
        },
        {
          title: 'O Christmas Tree',
          artist: 'Dylan Sitts',
          src: require('./assets/o-christmas-tree_dylan-sitts.mp3')
        },
        {
          title: 'Silent Night',
          artist: 'John Abbot',
          src: require('./assets/silent-night_john-abbot.mp3')
        },
        {
          title: 'The First Noel',
          artist: 'Matt Large',
          src: require('./assets/the-first-noel_matt-large.mp3')
        },
        {
          title: 'We Wish You A Merry Christmas',
          artist: 'Timothy Infinite',
          src: require('./assets/we-wish-you-a-merry-christmas_timothy-infinite.mp3')
        }
      ],
      player: new Audio()
    }
  },

  //When app loads, set the current state information to the information from the 0th element in the songs array
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    this.player.play();
  }
}
</script>

<style>
body{
  background-color: #F8E19E;
}
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
  }

  header{
    display: flex;
    flex-direction: row;
    justify-content: center;
    background-color: #121212;
    color: rgb(204, 32, 32);
    padding: 1vw;
  }

  section h2, h3{
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
</style>
