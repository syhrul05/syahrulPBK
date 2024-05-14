<script setup lang="ts">
import PersonalItem from './PersonalItem.vue'
</script>

<template>
  <PersonalItem>
    <template #heading>Nama</template>
    <!-- Isi nama Anda di sini -->
    Syahrul Ramadhan
  </PersonalItem>

  <PersonalItem>
    <template #heading>Alamat</template>
    <!-- Isi alamat Anda di sini -->
    Jl. Pahlawan Kerja Gg. Akasia, Pekanbaru
  </PersonalItem>

  <PersonalItem>
    <template #heading>Nomor Telepon</template>
    <!-- Isi nomor telepon Anda di sini -->
    +62 822 8380 1791
  </PersonalItem>

  <PersonalItem>
    <template #heading>Email</template>
    <!-- Isi email Anda di sini -->
    syhrulRmdh203@gmail.com
  </PersonalItem>

  <PersonalItem>
    <template #heading>Pekerjaan</template>
    <!-- Isi pekerjaan Anda di sini -->
    Mahasiswa Teknik Universitas Islam Riau 
  </PersonalItem>
</template>

<style scoped>
.personal-container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  background: #f0f0f0;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  text-align: center;
}

.personal-item {
  margin-bottom: 1rem;
}

.personal-item h2 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.personal-item p {
  font-size: 1rem;
  margin: 0;
}
</style>
