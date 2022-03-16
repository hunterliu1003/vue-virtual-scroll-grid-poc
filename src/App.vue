<script setup>
import { ref } from 'vue'
import Grid from 'vue-virtual-scroll-grid'

const currentScrollToIndex = ref()
const scrollToIndex = ref(10)

function setCurrentScrollToIndex (index) {
  currentScrollToIndex.value = undefined
  currentScrollToIndex.value = index
}
</script>

<template>
  <div :class="$style.button">
    <button class="scroll-to" @click="() => setCurrentScrollToIndex(scrollToIndex)">Scroll to</button>
    <input type="number" v-model="scrollToIndex" />
  </div>
  <div :class="$style['grid-container']">
    <Grid
      :length="100"
      :pageProvider="async (pageNumber, pageSize) => Array(pageSize).fill('x')"
      :pageSize="40"
      :scrollTo="currentScrollToIndex"
      :class="$style.grid"
    >
      <template v-slot:default="{ item, index, style }">
        <div :style="style" :class="$style['grid-item']">{{ item }}: {{ index }}</div>
      </template>
    </Grid>
  </div>
</template>

<style module>
.button {
  margin: 100px 0;
}
.grid-container {
  width: 100%;
  height: 300px;
  overflow: auto;
}

.grid {
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: repeat(2, 1fr);
  padding: 1rem;
  border: 1px solid gray;
}
.grid-item {
  border: 1px solid gray;
}
</style>