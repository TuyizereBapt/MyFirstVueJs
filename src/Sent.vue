<template>
    <div class="inbox-body">
        <app-messages :messages="sentMessages"></app-messages>
    </div>
</template>
<script>
import Messages from "./Messages.vue";

export default {
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  computed: {
    sentMessages() {
      return this.data.filter(function(message) {
        return message.type == "outgoing" && !message.isDeleted;
      });
    }
  },
  components: {
    appMessages: Messages
  }
};
</script>
