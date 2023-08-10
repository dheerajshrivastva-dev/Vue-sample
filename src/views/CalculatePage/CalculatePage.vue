<template>
  <div>
    <h1>data {{ data }}</h1>
    <h1>store count {{ counter.count }}</h1>
    <h2>2x store count {{ counter.doubleCount }}</h2>
    <button @click="counter.increment">increment</button>
    <h1>{{selectedData.name}}</h1>
    <div class="container" >
      <div
        class="card"
        :class="{ 'selected': data.id === selectedData.id }"
        v-for="data in sampleData"
        :key="data.id"
        @click="handleSelectedData(data.id)"
      >
        <div class="card-header">
          <h2 class="card-title">{{data.name}}</h2>
        </div>
        <div class="card-body">
          <slot>age: {{data.age}}</slot>
          <slot>email: {{data.email}}</slot>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
import { useCounterStore } from '@/stores/counter'
const counter = useCounterStore()

export default defineComponent({
  setup() {
    const data = ref(7)
    const sampleData = [
    { id: 0, name: 'Liam Doe', age: 40, email: 'liam@example.com' },
      { id: 1, name: 'John Doe', age: 30, email: 'john@example.com' },
      { id: 2, name: 'Jane Smith', age: 28, email: 'jane@example.com' },
      { id: 3, name: 'Michael Johnson', age: 35, email: 'michael@example.com' },
      { id: 4, name: 'Emily Brown', age: 25, email: 'emily@example.com' },
      { id: 5, name: 'William Davis', age: 40, email: 'william@example.com' },
      { id: 6, name: 'Olivia Wilson', age: 22, email: 'olivia@example.com' },
    ];
    const selectedData = ref(sampleData[0]);
    const handleSelectedData = (id: number) => {
      selectedData.value = sampleData[id % (sampleData.length)]
    }

    return {
      data,
      counter,
      sampleData,
      selectedData,
      handleSelectedData
    }
  }
})
</script>
<style>
.button {
  border-radius: 4px;
  padding: 8px 16px;
  background-color: teal;
  color: whitesmoke;
}

.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  max-width: 90%;
  max-height: 90%;
  overflow: auto;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.close-modal-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #f0f0f0;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

.open-modal-button {
  margin: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  color: white;
  cursor: pointer;
}

.container {
  display: grid;
  flex-wrap: wrap;
  grid-template-columns: repeat(2, 1fr);
}

.selected {
  outline: 2px solid pink;
}
.card {
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin: 10px;
  padding: 10px;
}

.card-header {
  background-color: #08f6fe34;
  border-bottom: 1px solid #ccc;
  padding: 5px 16px;
  border-radius: 4px 4px 0 0;
}

.card-title {
  margin: 0;
  padding: 0;
  font-size: 1.2em;
}

.card-body {
  padding: 10px 0;
}
</style>
