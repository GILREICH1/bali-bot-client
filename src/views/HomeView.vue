<template>
  <div class="wrapper">
    <div class="messages-view-overlay"></div>
    <messages-view class="messages-view"
      :messageLoading="messageLoading" :messages="messages" />
    <form class="home-view-input-bar" @submit.prevent="submitHandler">
      <n-space vertical>
        <n-input :disabled="inputDisabled" type="text"
          v-model:value="inputValue" round placeholder="Hello"
          ref="inputInstRef">
          <template #prefix>
            {{ "👋" }}
          </template>
        </n-input>
      </n-space>
    </form>
  </div>
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
    const inputInstRef = ref(null);
    return {
      inputInstRef,
      inputValue: ref(null),
      handleFocus() {
        console.log(inputInstRef.value?.focus);
        inputInstRef.value?.focus();
      },
    };
  },

  methods: {
    submitHandler() {
      if (this.inputValue) {
        const newMessage = {
          sender: "user",
          text: this.inputValue,
        };

        this.messages = [...this.messages, newMessage];
        this.inputValue = "";
        setTimeout(() => {
          this.getBotMessage();
        }, 400);
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
        this.handleFocus();
      }, 800);
    },
  },
};
</script>

<style>
.wrapper {
  position: relative;
}

.messages-view {
  top: 10rem;
  height: 70vh;
  display: flex;
  flex-direction: column;
  gap: 12px;
  overflow: scroll;
}

.messages-view-overlay {
  position: absolute;
  height: 70vh;
  top: 10rem;
  background: linear-gradient(rgb(255, 255, 255), rgba(255, 255, 255, 0));
  z-index: 100;
  width: 100%;
  overflow: hidden;
}

.home-view-input-bar {
  width: 70vw;
  bottom: 5px;
  position: fixed;
}
</style>
