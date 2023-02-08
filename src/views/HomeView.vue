<template>
  <main>
    <messages-view :messages="messages" />
    <form @submit.prevent="submitHandler">
      <n-space vertical>
        <n-input autofocus type="text" v-model:value="value" round
          placeholder="Hello">
          <template #prefix>
            {{ "👋" }}
          </template>
        </n-input>
      </n-space>
    </form>
  </main>
</template>

<script>
import MessagesView from "../components/MessagesView.vue";
import { NSpace, NInput } from "naive-ui";
import { ref } from 'vue';

export default {
  components: {
    NSpace,
    NInput,
    MessagesView,
  },

  data() {
    return {
      messages: ["hello", "test"],
    };
  },

  setup() {
    return {
      value: ref(null),
    };
  },

  methods: {
    submitHandler() {
      this.messages = [...this.messages, this.value];
      this.value = ''
    },
  },

};
</script>
