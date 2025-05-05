<script setup>
import { ref } from 'vue';

const showInput = ref(false);
const activities = ref([
  {
    text: 'Mengumpulkan UTS PBK',
    date: '2025-05-09',
    time: '23:00',
    done: false
  },
  {
    text: 'Rapat Organisasi',
    date: '2025-05-10',
    time: '10:30',
    done: true
  }
]);
</script>

<template>
  <div class="app-container">
    <div class="main-content">
      <div id="app" class="to-do">
        <div class="header-box">  
          <h1>Listify - Perencana Jadwal</h1>
          <p>Kelola kegiatan harianmu dengan efisien.</p>
        </div>
        
        <div class="activity-list">
          <h2>Kegiatan</h2>
          <ul>
            <li v-for="(activity, index) in activities" :key="index" class="task-item">
              <div class="task-content">
                <span>
                  <strong>{{ activity.text }} - </strong> 
                  <span class="task-details">
                    {{ activity.date || 'Tanpa tanggal' }} {{ activity.time ? '• ' + activity.time : '' }}
                  </span>
                </span>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>