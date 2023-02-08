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
      if (this.value) {
        const newMessage = {
          sender: "user",
          text: this.value,
        }

        this.messages = [...this.messages, newMessage];
        this.value = "";
        this.getBotMessage();
      }
    },
    async getBotMessage() {
      setTimeout(() => {
        const mockBotMessage = {
          sender: "bot",
          text: this.messages % 2 === 0 ? "yes" : "ok",
        };
        this.messages = [...this.messages, mockBotMessage];
      }, 800);
    },
  },
};
</script>
