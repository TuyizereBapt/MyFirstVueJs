<template>
    <div class="inbox-body">
        <app-messages :messages="importantMessages"></app-messages>
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
    importantMessages() {
      return this.data.filter(function(message) {
        return (
          message.type == "incoming" &&
          message.isImportant === true &&
          !message.isDeleted
        );
      });
    }
  },
  components: {
    appMessages: Messages
  }
};
</script>
