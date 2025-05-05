<script setup>
import { ref } from 'vue';

const showInput = ref(false);
const activities = ref([]);
</script>

<template>
  <div class="app-container">
    <div class="main-content">
      <div id="app" class="to-do">
        <div class="header-box">  
          <h1>Listify - Perencana Jadwal</h1>
          <p>Kelola kegiatan harianmu dengan efisien.</p>
        </div>
        
      </div>
    </div>
  </div>
</template>