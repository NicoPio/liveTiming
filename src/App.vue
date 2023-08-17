<template>
  <header>


    <div v-if="racers.length">
      <TransitionGroup tag="ul" name="fade" class="liveTimingWrapper">
        <liveTimingCard v-for="(racer, i) in racers" :key="racer.name" :racer="racer" :position="i + 1"
          :style="{ order: getPosition(racer.lapTime) }" />
      </TransitionGroup>
    </div>
    <button @click=" changePositions()">Change positions</button>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>


<script setup>
import { ref } from 'vue'
import liveTimingCard from './components/liveTimingCard.vue'

const racers = ref([]);

for (let i = 1; i <= 10; i++) {
  racers.value.push({
    name: `Racer ${i}`,
    lapTime: Math.floor(Math.random() * 100) + 1
  });
}

racers.value.sort((a, b) => a.lapTime - b.lapTime);


function changePositions() {
  racers.value.forEach((racer) => {
    racer.lapTime = Math.floor(Math.random() * 100) + 1;
    racers.value.sort((a, b) => a.lapTime - b.lapTime)
  })
}

function getPosition(lapTime) {
  return racers.value.findIndex((racer) => racer.lapTime === lapTime) + 1;
}

</script>



<style scoped lang="scss">
.liveTimingWrapper {
  position: relative;
  width: 600px;
  display: flex;
  flex-direction: column;
}

.fade-move,
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}

.fade-leave-active {
  position: absolute;
}
</style>
