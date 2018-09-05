<template>
    <div class="inbox-body">
        <div class="mail-option">
            <button class="btn btn-primary" @click="navigateBack">
                <i class="fa fa-arrow-left" aria-hidden="true"></i>&nbsp; Back
            </button>

            <button class="btn btn-danger" @click="data.isDeleted = true" :disabled="data.isDeleted">
                <i class="fa fa-trash-o"></i>&nbsp; {{ data.isDeleted ? 'Deleted' : 'Delete' }}
            </button>

            <template v-if="typeof data.isRead !== 'undefined'">
                <button class="btn btn-primary" @click="data.isRead = false" :disabled="!data.isRead">
                    <i class="fa fa-envelope-open" aria-hidden="true"></i>&nbsp; Mark as unread
                </button>

                <button class="btn btn-primary" @click="data.isRead = true" :disabled="data.isRead">
                    <i class="fa fa-envelope" aria-hidden="true"></i>&nbsp; Mark as read
                </button>
            </template>
        </div>
        <p><strong>Date:</strong> {{ data.date.fromNow() }}</p>
        <p><strong>From:</strong> {{ data.from.name }} <{{ data.from.email }}></p>
        <hr>
        <div class="message" v-html="data.content"></div>

        <div v-if="data.attachments.length > 0" class="attachments">
            <h4>Attachments</h4>

            <ul>
                <li v-for="(attachment,index) in data.attachments" :key="index">
                    <i class="fa fa-paperclip"></i> {{ attachment.fileName }} ({{ attachment.size | formatBytes }})
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
import { eventBus } from "./main";
export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  activated() {
    if (typeof this.data.isRead !== "undefined") {
      this.data.isRead = true;
    }
  },
  filters: {
    formatBytes(bytes) {
      if (bytes == 0) {
        return "0 Bytes";
      }

      let decimals = 2;
      let k = 1000;
      let dm = decimals + 1 || 3;
      let sizes = ["Bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB"];
      let i = Math.floor(Math.log(bytes) / Math.log(k));

      return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + " " + sizes[i];
    }
  },
  methods: {
    navigateBack() {
      let previousView = this.$parent.previousView;
      eventBus.$emit("changeView", {
        title: previousView.title,
        tag: previousView.tag,
        data: previousView.data
      });
    }
  }
};
</script>
