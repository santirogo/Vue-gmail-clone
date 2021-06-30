<template>
  <div class="modal">
    <div class="overlay" @click="$emit('closeModal')"></div>
    <div class="modal-card">
      <slot />
    </div>
  </div>
</template>

<script>
  export default {
    emits: ['closeModal'],
    created() {
      let onKeydown =  (event) => {
        if (event.key === 'Escape') {
          this.$emit('closeModal');
        }
      }
      window.addEventListener('keydown', onKeydown)
    }
  }
</script>

<style lang="scss" scoped>

</style>