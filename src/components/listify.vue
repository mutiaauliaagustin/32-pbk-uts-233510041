<script setup>
import { ref } from 'vue';
import { computed } from 'vue';

const showInput = ref(false);
const newActivity = ref({
    text: '',
    date: '',
    time: '',
    done: false
});

const activities = ref([
    {
        text: 'Mengumpulkan UTS PBK',
        date: '2025-05-09',
        time: '23:00',
        done: false
    },
    {
        text: 'Rapat Organisasi',
        date: '2025-05-05',
        time: '10:30',
        done: true
    }
]);

function addActivity() {
    if (newActivity.value.text.trim() !== '') {
        activities.value.push({ ...newActivity.value });
        newActivity.value = { text: '', date: '', time: '', done: false };
        showInput.value = false;
    }
}

function deleteActivity(index) {
    const actualIndex = activities.value.indexOf(filteredByStatusActivities.value[index]);
    if (actualIndex !== -1) {
        activities.value.splice(actualIndex, 1);
    }
}

const statusFilter = ref('all'); 

const filteredByStatusActivities = computed(() => {
    if (statusFilter.value === 'all') {
        return activities.value;
    } else if (statusFilter.value === 'pending') {
        return activities.value.filter(activity => !activity.done);
    } else {
        return activities.value.filter(activity => activity.done);
    }
});

const filteredActivities = computed(() => {
    return filteredByStatusActivities.value;
});
</script>

<template>  
    <div class="app-container">
        <div class="main-content">
            <div id="app" class="to-do">
                <div class="header-box">  
                    <h1>Listify - Perencana Jadwal</h1>
                    <p>Kelola kegiatan harianmu dengan efisien.</p>
                </div>

                <div class="add">
                    <div @click="showInput = !showInput" class="clickable">
                        {{ showInput ? '✕ Batal' : '✚ Tambah Tugas' }}
                    </div>
                    <div 
                        class="item" 
                        :class="{ active: statusFilter === 'all' }" 
                        @click="statusFilter = 'all'"
                    >Semua</div>
                    <div 
                        class="item" 
                        :class="{ active: statusFilter === 'pending' }" 
                        @click="statusFilter = 'pending'"
                    >Tertunda</div>
                    <div 
                        class="item" 
                        :class="{ active: statusFilter === 'completed' }" 
                        @click="statusFilter = 'completed'"
                    >Selesai</div>
                </div>

                <div v-if="showInput" class="popup-modal">
                    <div class="popup-content">
                        <h3>Tambah Tugas Baru</h3>

                        <div class="popup-input">
                            <input v-model="newActivity.text" placeholder="Apa yang perlu dilakukan?" />
                            <input type="date" v-model="newActivity.date" />
                            <input type="time" v-model="newActivity.time" />
                        </div> 
                        
                        <div class="popup-btn">
                            <button @click="addActivity">Tambahkan</button>
                            <button @click="showInput = false">Batal</button>
                        </div>
                    </div>
                </div>

                <div class="activity-list">
                    <h2>Kegiatan</h2>
                    <p v-if="filteredActivities.length === 0" class="empty-state">
                        Tidak ada tugas untuk ditampilkan. Tambahkan tugas pertama untuk memulai!
                    </p>
                    <ul>
                        <li v-for="(activity, index) in filteredActivities" :key="index" class="task-item">
                            <div class="task-content">
                                <span :class="{ completed: activity.done }">
                                    <strong>{{ activity.text }}</strong> 
                                    <span class="task-details">
                                        {{ activity.date || 'Tanpa tanggal' }} {{ activity.time ? '• ' + activity.time : '' }}
                                    </span>
                                </span>
                            </div>
                            <div class="task-actions">
                                <input type="checkbox" v-model="activity.done" :id="'task-' + index"/>
                                <button @click="deleteActivity(index)" class="delete-btn" title="Hapus tugas">❌</button>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>