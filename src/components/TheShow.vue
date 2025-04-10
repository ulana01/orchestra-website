<template>
  <div class="music-container">
    <div class="music-header">
      <h1>THE SHOW</h1>
      <h2>CHOIRCHESTRA</h2>
    </div>

    <div class="tracklist">
      <div v-for="(song, index) in songs" :key="index" class="track-item" @click="playSong(index)">
        <img src="@/assets/theshow.jpeg" alt="Album Art" class="track-image" />
        <div class="track-info">
          <h3>{{ song.title }}</h3>
          <p>{{ song.author }}</p>
        </div>
        <span class="track-duration">{{ formatTime(song.duration) }}</span>
      </div>
    </div>

    <!-- Music Player -->
    <div class="music-player">
      <div class="player-info">
        <img src="@/assets/theshow.jpeg" alt="Cover" class="player-image" />
        <div class="song-info">
          <h3>{{ currentSong.title }}</h3>
          <p>{{ currentSong.author }}</p>
        </div>
      </div>

      <!-- Audio player -->
      <audio ref="audio" @timeupdate="updateTime" @ended="nextSong">
        <source :src="currentSong.src" type="audio/mp3" />
      </audio>

      <div class="controls-and-progress">
        <!-- Player Controls -->
        <div class="player-controls">
          <img src="@/assets/shuffle.png" alt="Shuffle" />
          <img src="@/assets/prev.png" alt="Previous" @click="prevSong" />
          <img :src="isPlaying ? require('@/assets/pause.png') : require('@/assets/play.png')" alt="Play/Pause" @click="togglePlay" />
          <img src="@/assets/next.png" alt="Next" @click="nextSong" />
          <img src="@/assets/repeat.png" alt="Repeat" />
        </div>

        <!-- Progress Bar -->
        <div class="progress-container">
          <span>{{ formatTime(currentTime) }}</span>
          <input type="range" v-model="progress" @input="seekAudio" />
          <span>{{ formatTime(currentSong.duration) }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      songs: [
      { title: "Rock Around the Clock", author: "Bill Haley", src: "https://orchestra-website-5e76d.web.app/audio/Rock_around.mp3", cover: "@/assets/theshow.jpeg", duration: 133 },
      { title: "Sarzhailau", author: "Nurgisa Tilendiyev", src: "https://orchestra-website-5e76d.web.app/audio/Sarzhailau.mp3", cover: "/covers/sarzhailau.jpg", duration: 201 },
      { title: "Aigyr", author: "ARO", src: "https://orchestra-website-5e76d.web.app/audio/Aigyr.mp3", cover: "/covers/aigyr.jpg", duration: 214 },
      { title: "Feelin' good", author: "Anthony Newley", src: "https://orchestra-website-5e76d.web.app/audio/Feeling_Good.mp3", cover: "/covers/feeling_good.jpg", duration: 292 },
      { title: "Heathens X Stranger Things", author: "Twenty One Pilots, Kyle Dixon", src: "https://orchestra-website-5e76d.web.app/audio/Heathens_Stranger_Things.mp3", cover: "/covers/heathens.jpg", duration: 239 },
      { title: "Qosh Bol", author: "Moldanazar", src: "https://orchestra-website-5e76d.web.app/audio/Qosh_bol.mp3", cover: "/covers/Qosh_bol.jpg", duration: 190 },
      { title: "Tuimedaq", author: "Kunzharyq", src: "https://orchestra-website-5e76d.web.app/audio/Tuimedaq.mp3", cover: "/covers/Tuimedaq.jpg", duration: 240 },
      { title: "Bring Me to Life", author: "Evanescence", src: "https://orchestra-website-5e76d.web.app/audio/Bring_me_to_life.mp3", cover: "@/assets/theshow.jpeg", duration: 225 },
      { title: "Gangsta's Paradise", author: "Coolio", src: "https://orchestra-website-5e76d.web.app/audio/Gangstas_Paradise.mp3", cover: "@/assets/theshow.jpeg", duration: 249 },
      { title: "Gashyqsyn ba X Zhauap ber", author: "Orda", src: "https://orchestra-website-5e76d.web.app/audio/Gashyqsyn_ba.mp3", cover: "@/assets/theshow.jpeg", duration: 193 },
      { title: "Kazakh Hip-Hop Medley", author: "Irina Kairatovna, SHIZA", src: "https://orchestra-website-5e76d.web.app/audio/Kazakh_hip-hop.mp3", cover: "@/assets/theshow.jpeg", duration: 264 },
      { title: "Lalala", author: "Naughty Boy", src: "https://orchestra-website-5e76d.web.app/audio/Lalala.mp3", cover: "@/assets/theshow.jpeg", duration: 218 },
      { title: "Take on me", author: "a-ha", src: "https://orchestra-website-5e76d.web.app/audio/Take_on_me.mp3", cover: "@/assets/theshow.jpeg", duration: 211 },
      { title: "The Greatest Show", author: "Benj Pasek, Justin Paul", src: "https://orchestra-website-5e76d.web.app/audio/The_greatest_show.mp3", cover: "@/assets/theshow.jpeg", duration: 247 },
      { title: "Uptown Funk", author: "Bruno Mars", src: "https://orchestra-website-5e76d.web.app/audio/Uptown_funk.mp3", cover: "@/assets/theshow.jpeg", duration: 253 },
      { title: "Where is The Love", author: "The Black Eyed Peas", src: "https://orchestra-website-5e76d.web.app/audio/Where_is_the_love.mp3", cover: "@/assets/theshow.jpeg", duration: 251 }

      ],
      currentSongIndex: 0,
      isPlaying: false,
      progress: 0,
      currentTime: 0
    };
  },
  computed: {
    currentSong() {
      return this.songs[this.currentSongIndex];
    }
  },
  methods: {
    playSong(index) {
      this.currentSongIndex = index;
      this.playAudio();
    },
    playAudio() {
      this.$nextTick(() => {  
        const audio = this.$refs.audio;
        if (!audio) {
          console.error("Audio element not found.");
          return;
        }
        audio.src = this.currentSong.src;
        audio.load();
        audio.play()
          .then(() => {
            this.isPlaying = true;
          })
          .catch(err => {
            console.error("Error playing audio:", err);
          });
      });
    },
    togglePlay() {
      this.$nextTick(() => {
        const audio = this.$refs.audio;
        if (!audio) {
          console.error("Audio element is not found.");
          return;
        }
        if (audio.paused) {
          audio.play();
          this.isPlaying = true;
        } else {
          audio.pause();
          this.isPlaying = false;
        }
      });
    },
    prevSong() {
      this.currentSongIndex = (this.currentSongIndex - 1 + this.songs.length) % this.songs.length;
      this.playAudio();
    },
    nextSong() {
      this.currentSongIndex = (this.currentSongIndex + 1) % this.songs.length;
      this.playAudio();
    },
    updateTime() {
      this.currentTime = this.$refs.audio.currentTime;
      this.progress = (this.currentTime / this.currentSong.duration) * 100;
    },
    seekAudio(event) {
      const newTime = (event.target.value / 100) * this.currentSong.duration;
      this.$refs.audio.currentTime = newTime;
      this.currentTime = newTime;
    },
    formatTime(seconds) {
      const min = Math.floor(seconds / 60);
      const sec = Math.floor(seconds % 60).toString().padStart(2, "0");
      return `${min}:${sec}`;
    }
  }
};
</script>

<style scoped>
.music-container {
  background: black;
  color: white;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.music-header {
  text-align: center;
  margin-bottom: 20px;
}

.music-header h1 {
  font-size: 36px;
}

.music-header h2 {
  font-size: 20px;
}

.tracklist {
  width: 90%;
  max-width: 600px;
  overflow-y: auto;
}

.track-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid white;
  cursor: pointer;
  transition: 0.3s;
}

.track-item:hover {
  background: rgba(255, 255, 255, 0.1);
}

.track-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

.track-info {
  flex: 1;
  margin-left: 10px;
}

.track-duration {
  font-size: 14px;
  color: gray;
}

.music-player {
  width: 100%;
  background: white;
  padding: 20px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  color: black;
  bottom: 0;
  gap: 160px;
}

.player-info {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.player-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.song-info {
  text-align: left;
}

.song-info h3 {
  margin-block: 8px;
}

.song-info p {
  margin: 0;
}

.controls-and-progress {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.player-controls {
  display: flex;
  align-items: center;
  gap: 30px;
  margin-bottom: 20px;
}

.player-controls img {
  width: 30px;
  height: 30px;
  cursor: pointer;
  transition: opacity 0.2s ease-in-out;
}

.player-controls img:hover {
  opacity: 0.7;
}

.progress-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-bottom: 10px;
}

input[type="range"] {
  width: 400px;
  height: 4px;
  background: #ccc;
  border-radius: 5px;
  cursor: pointer;
  margin: 0 10px;
  appearance: none;
}

input[type="range"]:focus {
  outline: none;
}

.time-info {
  display: flex;
  gap: 10px;
  font-size: 14px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .music-player {
    flex-direction: column;
    gap: 20px;
    padding: 15px;
  }
  
  .player-info {
    flex-direction: column;
    align-items: center;
    margin-bottom: 15px;
  }

  .song-info {
    text-align: center;
  }

  .controls-and-progress {
    gap: 10px;
  }

  .player-controls {
    gap: 20px;
  }
  
  input[type="range"] {
    width: 100%;
  }
}
</style>
