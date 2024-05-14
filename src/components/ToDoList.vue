<template>
  <div class="todo-container">
    <h1>Daftar Tugas</h1>
    <div class="input-container">
      <input v-model="tugasBaru" @keyup.enter="tambahTugas" placeholder="Tambahkan tugas baru" />
      <select v-model="prioritasBaru">
        <option value="Tinggi">Tinggi</option>
        <option value="Sedang">Sedang</option>
        <option value="Rendah">Rendah</option>
      </select>
      <button @click="tambahTugas" v-if="!isEditing">Tambah</button>
      <button @click="updateTugas" v-else>Update</button>
    </div>
    <ul>
      <li v-for="(tugas, index) in tugasList" :key="index" :class="{'task-item': true, 'priority-high': tugas.prioritas === 'Tinggi', 'priority-medium': tugas.prioritas === 'Sedang', 'priority-low': tugas.prioritas === 'Rendah'}">
        <span :class="{ selesai: tugas.selesai }" @click="toggleTugas(index)">
          {{ tugas.teks }} - <small>{{ tugas.prioritas }}</small>
        </span>
        <div class="actions">
          <button @click="editTugas(index)">Edit</button>
          <button @click="hapusTugas(index)">Hapus</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const tugasBaru = ref('');
const prioritasBaru = ref('Sedang');
const tugasList = ref<{ teks: string; selesai: boolean; prioritas: string }[]>([]);
const isEditing = ref(false);
const currentIndex = ref<number | null>(null);

const tambahTugas = () => {
  if (tugasBaru.value.trim()) {
    tugasList.value.push({ teks: tugasBaru.value, selesai: false, prioritas: prioritasBaru.value });
    resetInput();
  }
};

const editTugas = (index: number) => {
  tugasBaru.value = tugasList.value[index].teks;
  prioritasBaru.value = tugasList.value[index].prioritas;
  isEditing.value = true;
  currentIndex.value = index;
};

const updateTugas = () => {
  if (currentIndex.value !== null) {
    tugasList.value[currentIndex.value].teks = tugasBaru.value;
    tugasList.value[currentIndex.value].prioritas = prioritasBaru.value;
    resetInput();
  }
};

const resetInput = () => {
  tugasBaru.value = '';
  prioritasBaru.value = 'Sedang';
  isEditing.value = false;
  currentIndex.value = null;
};

const toggleTugas = (index: number) => {
  tugasList.value[index].selesai = !tugasList.value[index].selesai;
};

const hapusTugas = (index: number) => {
  tugasList.value.splice(index, 1);
};
</script>

<style scoped>
.todo-container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  background: #f0f0f0;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  text-align: center;
}

.input-container {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}

input, select {
  padding: 0.5rem;
  font-size: 1rem;
  margin-right: 0.5rem;
}

button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background: #358a5f;
}

ul {
  list-style-type: none;
  padding: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem;
  background: #fff;
  margin-bottom: 0.5rem;
  border-radius: 4px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}

.task-item span {
  cursor: pointer;
}

.task-item span.selesai {
  text-decoration: line-through;
  color: #bbb;
}

.task-item .actions {
  display: flex;
  gap: 0.5rem;
}

.task-item button {
  background: #ff6b6b;
  border: none;
  border-radius: 4px;
  padding: 0.2rem 0.5rem;
}

.task-item button:hover {
  background: #d9534f;
}

.task-item .actions button:first-child {
  background: #f0ad4e;
}

.task-item .actions button:first-child:hover {
  background: #ec971f;
}

.priority-high {
  border-left: 5px solid #ff0000;
}

.priority-medium {
  border-left: 5px solid #ffa500;
}

.priority-low {
  border-left: 5px solid #00ff00;
}
</style>
