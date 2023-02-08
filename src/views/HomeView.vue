<template>
  <main>
    <TheWelcome />
    <n-space vertical>
      <n-input round placeholder="Hello">
        <template #prefix>
          {{ "👋" }}
        </template>
      </n-input>
    </n-space>
  </main>
</template>

<script>
import TheWelcome from "../components/MessagesView.vue";
import { NSpace, NInput, NIcon } from "naive-ui";

export default {
  components: {
    NSpace,
    NIcon,
    NInput,
    TheWelcome,
  },
};
</script>
