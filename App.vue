<template>
  <div id="app">
    <header>
      <h1>Everly Christmas Music</h1>
    </header>
    <main>
      <div class="current-song-container">
        <div class="inner-container" id="inner-container-curr-song">
          <img class="main-thumbnail" :src="current.image" alt="">

          <div class="title-controls">
            <div class="title-artist">
              <h2 class="song-title">{{current.title}}</h2>
              <h3>{{current.artist}}</h3>
            </div>

            <div class="controls">
              <div id="prev" @click="previous"><img src="https://cdn4.iconfinder.com/data/icons/glyphs/24/icons_next-256.png" alt=""></div>
              <div id="play" class="playPause" v-if="!isPlaying" @click="play"><img src="https://cdn4.iconfinder.com/data/icons/glyphs/24/icons_play-256.png" alt=""></div>
              <div id="pause" class="playPause" v-else @click="pause"><img src="https://cdn3.iconfinder.com/data/icons/music-player-controls/100/music_pause_stop_control_play-256.png" alt=""></div>
              <div id="next" @click="next"><img src="https://cdn4.iconfinder.com/data/icons/glyphs/24/icons_next-256.png" alt=""></div>
            </div>
          </div>
        </div>
      </div>

      <div class="playlist-container">
        <div class="inner-container" id="inner-container-playlist">
          <div class="list-container">
            <!-- Loop through songs state and display a button for each of them that, when clicked, will play that specific song -->
            <div v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.song) ? 'song playing' : 'song'">
              <img class="mini-thumbnail" :src="song.image" alt="">
              <p>{{song.title}} - {{song.artist}}</p>
            </div>
          </div>
        </div>
      </div>
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
          image: require('./assets/deck-the-halls-image.jpg'),
          title: 'Deck The Halls',
          artist: 'Megan Wooffard',
          src: require('./assets/deck-the-halls_megan-wooffard.mp3')
        },
        {
          image: require('./assets/jingle-bells-image.jpg'),
          title: 'Jingle Bells',
          artist: 'Jobii',
          src: require('./assets/jingle-bells_jobii.mp3')
        },
        {
          image: require('./assets/joy-to-the-world-image.png'),
          title: 'Joy to the World',
          artist: 'Timothy Infinite',
          src: require('./assets/joy-to-the-world_timothy-infinite.mp3')
        },
        {
          image: require('./assets/o-christmas-tree-image.png'),
          title: 'O Christmas Tree',
          artist: 'Dylan Sitts',
          src: require('./assets/o-christmas-tree_dylan-sitts.mp3')
        },
        {
          image: require('./assets/silent-night-image.jpg'),
          title: 'Silent Night',
          artist: 'John Abbot',
          src: require('./assets/silent-night_john-abbot.mp3')
        },
        {
          image: require('./assets/the-first-noel-image.png'),
          title: 'The First Noel',
          artist: 'Matt Large',
          src: require('./assets/the-first-noel_matt-large.mp3')
        },
        {
          image: require('./assets/we-wish-you-a-merry-christmas-image.jpg'),
          title: 'We Wish You A Merry Christmas',
          artist: 'Timothy Infinite',
          src: require('./assets/we-wish-you-a-merry-christmas_timothy-infinite.mp3')
        }
      ],
      player: new Audio()
    }
  },

  //An object of methods that we will use to control the music
  methods: {
    //play method that will set this.current to the selected song and begin playing it.
    //Sets isPlaying to true so that the active button is set to "Pause"
    play(song) {
      if (typeof song.src != "undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },

    //pause method that will pause the current song and change isPlaying to false so that the button text
    //changes to  "Play"
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    //increment index by 1, which will set the current song to the next element in songs list. If index is greater than element
    //number, then go to 0
    //Then set it to current song and play current song
    next() {
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },

    //decrement index by 1, which will set the current song to the previous element in songs list. If index is less than 0,
    //then go to the last element in the songs list
    //Then set it to current song and play current song
    previous() {
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },

  //When app loads, set the current state information to the information from the 0th element in the songs array
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
}
</script>

<style>
  body{
    background: #cb2d3e;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #ef473a, #cb2d3e);  /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #ef473a, #cb2d3e); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  }

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
    color: rgba(250,250,250,1)
  }

  header{
    display: flex;
    flex-direction: row;
    justify-content: center;
    padding: 1vw;
    height: 10vh;
  }

  header h1{
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  #prev img{
      transform: rotate(180deg);
    }

  @media screen and (max-width: 799px) {
    header{
      border-bottom: 1px rgba(0,0,0,0.25) solid;
    }

    main{
      display: flex;
      flex-direction: column-reverse;
      height: 90vh;
    }

    .current-song-container{
      height: 20vh;
    }

    #inner-container-curr-song{
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
    }

    .title-controls{
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      height: 75%;
      width: 70vw;
    }

    .main-thumbnail{
      height: 15vh;
      width: 15vh;
      background-color: #fff;
      border-radius: 5px;
      object-fit: cover;
    }

    .title-artist{
      height: 10vh;
      margin-left: 10px;
    }

    .title-artist h2{
      font-size: 150%;
    }

    .title-artist h3{
      font-size: 90%;
    }

    .controls{
      display: flex;
      flex-direction: row;
      justify-content: space-around;
      align-items: center;
      height: 5vh;
    }

    .controls img{
      height: 10vw;
      width: 10vw;
      cursor: pointer;
    }

    .playlist-container{
      height: 70vh;
      display: flex;
      flex-direction: column;
      justify-content: center;

      border-bottom: 1px rgba(0,0,0,0.25) solid;
    }

    .list-container{
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      cursor: pointer;
    }

    #inner-container-playlist{
      height: 100%;
    }

    .list-container div{
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
      align-items: center;
      text-align: left;
      height: inherit;
      background-color: rgba(0,0,0,0);
      border-radius: 5px;
      padding: 5px;

      transition: 0.2s ease;
    }

    .list-container div:hover{
      background-color: rgba(0,0,0,0.25);
    }

    .mini-thumbnail{
      height: 15vw;
      width: 15vw;
      margin-right: 1vw;
      background-color: #fff;
      border-radius: 3px;
      object-fit: cover;
    }
  }

  @media screen and (min-width: 800px){
    main{
      display: flex;
      height: 90vh;
      flex-direction: row;
    }

    .current-song-container{
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    .inner-container{
      height: 75%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    .main-thumbnail{
      height: 30vw;
      width: 30vw;
      background-color: #fff;
      margin-left: auto;
      margin-right: auto;
      border-radius: 5px;
      object-fit: cover;
    }

    .controls{
      margin-left: auto;
      margin-right: auto;
      display: flex;
      flex-direction: row;
      justify-content: space-around;
      width: 40%;
    }

    .controls img{
      height: 5vw;
      width: 5vw;
      cursor: pointer;
    }

    .playlist-container{
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    .list-container{
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      cursor: pointer;
    }

    .list-container div{
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
      align-items: center;
      text-align: left;
      height: inherit;
      width: 95%;
      font-size: 1.25vw;
      background-color: rgba(0,0,0,0);
      border-radius: 5px;
      padding: 5px;

      transition: 0.2s ease;
    }

    .list-container div:hover{
      background-color: rgba(0,0,0,0.25);
    }

    .mini-thumbnail{
      height: 5vw;
      width: 5vw;
      margin-right: 1vw;
      background-color: #fff;
      border-radius: 3px;
      object-fit: cover;
    }

    div h2, h3{
      display: flex;
      flex-direction: row;
      justify-content: center;
    } 
  }
</style>
