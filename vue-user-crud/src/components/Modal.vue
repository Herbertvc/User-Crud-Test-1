<template>
  <div class="modal is-active">
    <div class="modal-background" @click="$emit('closeModal')"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">
          <slot name="modal-title"></slot>
        </p>
        <button class="delete" @click="$emit('closeModal')"></button>
      </header>
      <section class="modal-card-body">
        <slot name="modal-body"></slot>
      </section>
      <footer class="modal-card-foot">
        <a class="button is-primary" :class="{ 'is-disabled': !isFormCompleted }" >Save changes</a>
        <a class="button" @click="$emit('closeModal')">Cancel</a>
      </footer>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'modal',
    props: ['isFormCompleted'],
  }
</script>

<style language="scss" scoped>
  
</style>