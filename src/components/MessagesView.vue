<template>
  <n-space vertical>
    <template :key="i" v-for="(message, i) in messages">
      <n-card>
        {{ message }}
      </n-card>
    </template>
  </n-space>
</template>

<script>
import { NCard, NSpace } from "naive-ui";

export default {
  components: {
    NCard,
    NSpace,
  },
  props: {
    messages: Array,
  },
};
</script>

<style scoped>
.n-card {
  max-width: 300px;
}
</style>
