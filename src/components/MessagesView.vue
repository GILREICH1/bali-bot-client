<template>
  <div class="messages">
    <template :key="i" v-for="(message, i) in messages">
      <n-card size="small" :bordered="false"
        :class="`${message.sender} message`">
        {{ message.text }}
      </n-card>
    </template>
  </div>
</template>

<script>
import { NCard } from "naive-ui";

export default {
  components: {
    NCard,
  },
  props: {
    messages: Array,
  },
};
</script>

<style scoped>
.bot {
  background-color: green;
}

.messages {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.user {
  align-self: end;
  background-color: bisque;
}

.message {
  min-width: 50px;
  max-width: 200px;
}
</style>
