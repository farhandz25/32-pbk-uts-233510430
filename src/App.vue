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
    </template>