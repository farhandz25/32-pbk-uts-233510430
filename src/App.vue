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
    </template>