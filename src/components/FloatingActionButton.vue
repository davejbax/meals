<template>
  <div class="fab-container">
    <button
      class="fab"
      @click="(e) => this.$emit('click', e)"
    >
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
  name: 'FloatingActionButton'
}
</script>

<style>
.fab-container {
  position: absolute;

  right: 2rem;
  bottom: 2rem;
}

.fab {
  position: relative;
  overflow: hidden;

  width: 2em;
  height: 2em;
  border-radius: 50%;

  border: none;
  background: #e61a49;
  color: white;
  font-size: 2rem;

  cursor: pointer;

  box-shadow: 0 0.4rem 0.8rem rgba(0, 0, 0, 0.5);
  transition: background 0.1s ease-in-out;
}

.fab:hover {
  background-color: #ac0022;
}

.fab:focus {
  outline: none;
}

/* Ripple effect */
.fab:after {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  content: '';
  pointer-events: none;

  background-image: radial-gradient(circle, #000 10%, transparent 10.1%);
  background-repeat: no-repeat;
  background-position: 50%;

  transform: scale(10);
  opacity: 0;
  transition: transform 0.5s, opacity 1s;
}

.fab:active:after {
  transform: scale(0);
  opacity: 0.3;
  transition: 0s;
}
</style>
