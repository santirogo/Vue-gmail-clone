<template>
  <div class="bulk-action-bar">
    <span class="checkbox">
      <input
        type="checkbox"
        :checked="allEmailsSelected"
        :class="[someEmailsSelected ? 'partial-check' : '']"
        @click="bulkSelect"
      />
    </span>
    <span class="buttons">
      <button 
        @click="emailSelection.markRead()"
        :disabled="[...emailSelection.emails].every(e => e.read)"
      >
        Mark Read
      </button>
      <button 
        @click="emailSelection.markUnread()"
        :disabled="[...emailSelection.emails].every(e => !e.read)"
      >
        Mark Unread
      </button>
      <button 
        @click="emailSelection.archive()"
        :disabled="numberSelected === 0"
      >
        Archive
      </button>
    </span>
  </div>
</template>

<script>
import useEmailSelection from "@/composables/use-email-selection.js";
export default {
  setup() {
    return {
      emailSelection: useEmailSelection(),
    }; 
  },
  props: {
    emails: {
      type: Array,
      required: true,
    },
  },
  computed: {
    numberSelected () {
      return this.emailSelection.emails.size;
    },
    allEmailsSelected () {
      return this.numberSelected === this.emails.length;
    },
    someEmailsSelected () {
      return this.numberSelected > 0 && this.numberSelected < this.emails.length;
    }
  },
  methods: {
    bulkSelect () {
      if (this.allEmailsSelected) {
        this.emailSelection.clear();
      } else {
        this.emailSelection.addMultiple(this.emails);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
</style>