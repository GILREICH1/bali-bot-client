<template>
  <messages-view :messages="messages" />
  <form class="home-view-input-bar" @submit.prevent="submitHandler">
    <n-space vertical>
      <n-input autofocus type="text" v-model:value="value" round
        placeholder="Hello">
        <template #prefix>
          {{ "👋" }}
        </template>
      </n-input>
    </n-space>
  </form>
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
      messages: [],
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
          text: this.messages.length % 2 === 0 ? "yes" : "ok",
        };
        this.messages = [...this.messages, mockBotMessage];
      }, 800);
    },
  },
};
</script>

<style>
.home-view-input-bar {
  width: 70vw;
  bottom: 5px;
  position: fixed;
}
</style>
