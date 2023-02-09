<template>
  <div>
    <template :key="i" v-for="(message, i) in messages">
      <n-card size="small" :bordered="false"
        :class="generateClasses(message, i)">{{
          message.text
        }}</n-card>
    </template>
    <n-card v-if="messageLoading" size="small" :bordered="false"
      class="message">
      <n-skeleton :repeat="2" text width="60%" />
    </n-card>
  </div>
</template>

<script>
import { NCard, NSkeleton } from "naive-ui";

export default {
  components: {
    NCard,
    NSkeleton,
  },
  props: {
    messages: Array,
    messageLoading: Boolean,
  },
  updated() {
    this.scrollToElement();
  },
  methods: {
    generateClasses(message, i) {
      let classNames = ['message', message.sender];
      if (i === this.messages.length - 1) classNames.push('latestMessage')

      return classNames;
    },
    scrollToElement() {
      const lastestMessage = this.$el.querySelector(".latestMessage");
      lastestMessage.scrollIntoView({ behavior: 'smooth' })
    },
  },
};
</script>

<style scoped>
.latestMessage {
  background-color: rgb(0, 0, 0) !important;
}

.bot {
  background-color: rgb(200, 255, 200);
}

.user {
  align-self: end;
  background-color: rgb(150, 255, 200);
}

.message {
  min-width: 20px;
  max-width: 200px;
}
</style>
