<template>
    <div class="personal-item">
      <h2><slot name="heading"></slot></h2>
      <p><slot></slot></p>
    </div>
  </template>
  
  <style scoped>
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
  