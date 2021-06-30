<template>
  <div class="email-display">
    <div>
      <button @click="toggleArchive">{{ email.archived ? 'Move to Inbox' : 'Archive' }}</button>
      <button @click="toggleRead">{{ email.read ? 'Mark Unread' : 'Mark Read' }}</button>
      <button @click="goNewer">Newer</button>
      <button @click="goOlder">Older</button>
    </div>
    <h2 class="mb-0">
      Subject: <strong>{{ email.subject }}</strong>
    </h2>
    <div>
      <em
        >From {{ email.from }} on
        {{ format(new Date(email.sentAt), "MMM do yyyy") }}</em
      >
    </div>
    <div v-html="marked(email.body)"></div>
  </div>
</template>

<script>
import { format } from "date-fns";
import marked from 'marked';
import axios from 'axios';
export default {
  setup(props) {
    console.log("props received:", props);
    return {
      format,
      marked
    };
  },
  props: {
    email: {
      type: Object,
      required: true,
    },
  },
  methods: {
    toggleRead () {
      this.$emit('changeEmail', {toggleRead: true, save: true});
    },
    toggleArchive () {
      this.$emit('changeEmail', {toggleArchive: true, save: true, closeModal: true});
    },
    goNewer () {
      this.$emit('changeEmail', {changeIndex: -1});
    },
    goOlder () {
      this.$emit('changeEmail', {changeIndex: 1});
    }
  }
};
</script>

<style scoped>
</style>