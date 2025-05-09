<template>
  <div :data-theme="theme" class="app-container">
    <div class="header">
      <h1 class="title">🎵 My Playlist Lagu</h1>
      <button class="theme-toggle" @click="toggleTheme">
        {{ theme === 'light' ? '🌙 Dark Mode' : '☀️ Light Mode' }}
      </button>
    </div>

    <form class="form" @submit.prevent="addSong">
      <input class="input" v-model="newSong" placeholder="Tambah lagu kamu..." />
      <button class="btn" type="submit">Tambah</button>
    </form>

    </div>

    <div class="filters">
      <button :class="{ active: filter === 'all' }" @click="filter = 'all'">Semua</button>
      <button :class="{ active: filter === 'active' }" @click="filter = 'active'">Belum</button>
      <button :class="{ active: filter === 'done' }" @click="filter = 'done'">Selesai</button>
    </div>

    <div class="progress-bar">
      <div class="progress" :style="{ width: progress + '%' }"></div>
    </div>

    <div class="focus-mode">
      <label>
        <input type="checkbox" v-model="focusMode" />
        Fokus hanya lagu belum selesai
      </label>
    </div>

    <transition-group name="fade-slide" tag="ul" class="song-list">
      <li class="song-item" v-for="(song, index) in displayedSongs" :key="index">
        <input type="checkbox" v-model="song.done" />
        <span :class="{ done: song.done }">{{ song.name }}</span>
        <button class="delete-btn" @click="deleteSong(index)">🗑️</button>
      </li>
    </transition-group>

    <!-- Statistik penggunaan -->
    <div class="stats">
      <p>Total lagu: {{ songs.length }}</p>
      <p>Selesai: {{ completed }}</p>
      <p>Belum selesai: {{ remaining }}</p>
    </div>

    <div class="footer">
      <span>{{ remaining }} lagu tersisa</span>
      <button class="btn danger-btn" @click="clearCompleted">Hapus yang selesai</button>
    </div>

    <!-- Audio element -->
    <audio ref="clickSound" src="https://www.myinstants.com/media/sounds/mouse-click.mp3"></audio>
    
    </template>

<script>
export default {
  data() {
    return {
      theme: localStorage.getItem('theme') || 'light',
      newSong: '',
      songs: [],
      filter: 'all',
      focusMode: false,
    };
  },
computed: {
    filteredSongs() {
      if (this.filter === 'active') return this.songs.filter(s => !s.done);
      if (this.filter === 'done') return this.songs.filter(s => s.done);
      return this.songs;
    },
    displayedSongs() {
      return this.focusMode
        ? this.filteredSongs.filter(s => !s.done)
        : this.filteredSongs;
    },
    remaining() {
      return this.songs.filter(s => !s.done).length;
    },
    completed() {
      return this.songs.filter(s => s.done).length;
    },
    progress() {
      if (this.songs.length === 0) return 0;
      const doneCount = this.songs.filter(s => s.done).length;
      return Math.round((doneCount / this.songs.length) * 100);
    },
  },
methods: {
    toggleTheme() {
      this.playClick()
      this.theme = this.theme === 'light' ? 'dark' : 'light';
      localStorage.setItem('theme', this.theme);
    },
    addSong() {
      if (this.newSong.trim()) {
        this.songs.push({ name: this.newSong.trim(), done: false });
        this.newSong = '';
        this.playClick();
      }
    },
    deleteSong(index) {
      this.songs.splice(index, 1);
      this.playClick();
    },
  },
};
</script>