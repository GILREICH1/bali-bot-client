<template>
  <messages-view class="messages-view"
    :messageLoading="messageLoading" :messages="messages" />
  <form class="home-view-input-bar" @submit.prevent="submitHandler">
    <n-space vertical>
      <n-input :passively-activated="true" :disabled="inputDisabled"
        autofocus type="text" v-model:value="value" round
        placeholder="Hello" ref="input">
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
import { ref } from "vue";
import { mockBotMessages } from '../assets/mocks';

export default {
  components: {
    NSpace,
    NInput,
    MessagesView,
  },

  data() {
    return {
      messages: mockBotMessages,
      inputDisabled: false,
      messageLoading: false,
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
        };

        this.messages = [...this.messages, newMessage];
        this.value = "";
        this.getBotMessage();
      }
    },
    async getBotMessage() {
      this.inputDisabled = true;
      this.messageLoading = true;
      setTimeout(() => {
        const mockBotMessage = {
          sender: "bot",
          text: this.messages.length % 2 === 0 ? "yes" : "ok",
        };
        this.messages = [...this.messages, mockBotMessage];
        this.messageLoading = false;
        this.inputDisabled = false;
        this.$refs.input.focus();
      }, 200);
    },
  },
};
</script>

<style>
.messages-view {
  top: 10rem;
  height: 70vh;
  display: flex;
  flex-direction: column;
  gap: 12px;
  overflow: scroll;
}


.home-view-input-bar {
  width: 70vw;
  bottom: 5px;
  position: fixed;
}
</style>
