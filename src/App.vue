<template>
  <div class="widget-container">
    <div class="widget-header">
      <h1>{{ title }}</h1>
      <p class="subtitle">Interactive Vue Widget</p>
    </div>
    
    <div class="widget-content">
      <div class="counter-section">
        <h2>Counter</h2>
        <div class="counter-display">
          <button @click="decrement" class="btn btn-minus">-</button>
          <span class="counter-value">{{ count }}</span>
          <button @click="increment" class="btn btn-plus">+</button>
        </div>
        <button @click="reset" class="btn btn-reset">Reset</button>
      </div>

      <div class="message-section">
        <h2>Messages</h2>
        <input 
          v-model="message" 
          @keyup.enter="addMessage"
          placeholder="Enter a message..."
          class="message-input"
        />
        <button @click="addMessage" class="btn btn-add">Add</button>
        <ul class="message-list">
          <li v-for="(msg, index) in messages" :key="index" class="message-item">
            {{ msg }}
          </li>
        </ul>
      </div>
    </div>

    <div class="widget-footer">
      <p>Time: {{ currentTime }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';

export default {
  name: 'App',
  setup() {
    const title = ref('Vue Widget');
    const count = ref(0);
    const message = ref('');
    const messages = ref([]);
    const currentTime = ref(new Date().toLocaleTimeString());
    let timeInterval = null;

    const increment = () => {
      count.value++;
    };

    const decrement = () => {
      count.value--;
    };

    const reset = () => {
      count.value = 0;
    };

    const addMessage = () => {
      if (message.value.trim()) {
        messages.value.push(message.value);
        message.value = '';
      }
    };

    onMounted(() => {
      timeInterval = setInterval(() => {
        currentTime.value = new Date().toLocaleTimeString();
      }, 1000);
    });

    onUnmounted(() => {
      if (timeInterval) {
        clearInterval(timeInterval);
      }
    });

    return {
      title,
      count,
      message,
      messages,
      currentTime,
      increment,
      decrement,
      reset,
      addMessage,
    };
  },
};
</script>

