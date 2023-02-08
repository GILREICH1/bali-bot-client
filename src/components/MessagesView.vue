<template>
  <template :key="i" v-for="(message, i) in messages">
    <n-card>
      {{ message }}
      <template #footer>
        {{ "footer" }}
      </template>
    </n-card>
  </template>
</template>

<script>
import { NCard } from "naive-ui";

export default {
  components: {
    NCard
  },
  data() {
    return {
      messages: ["hello", "test"],
    };
  },
};
</script>

<style scoped>
.n-card {
  max-width: 300px;
}
</style>
