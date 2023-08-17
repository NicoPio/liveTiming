<template>
  <li class="card">
    <div class="position">{{ position }}</div>
    <div class="name">{{ racer.name }}</div>
    <div class="lapTime">{{ racer.lapTime }} sec.</div>
  </li>
</template>


<script setup>
defineProps({
  racer: {
    type: Object,
    required: true
  },
  position: {
    type: Number,
    required: true
  }
})
</script>


<style scoped lang="scss">
.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  border: 1px solid #ccc;
  margin-bottom: 1rem;
  border-radius: 5px;
  width: 100%;
  transition: all 1s ease-in-out;

  .position {
    font-size: 1.5rem;
    font-weight: bold;
  }
}
</style>
