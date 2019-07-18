<template>
  <transition :duration="150" name="modal-anim">
    <div
      :class="'modal-container'"
      v-if="open"
      ref="modalContainer"
      @mousedown="onBeginClick"
      @mouseup="onEndClick"
      @click="onClickContainer"
    >
      <aside :class="['modal', modalClass]">
        <header>
          <h2 class="inline">{{ title }}</h2>
          <button @click="() => this.$emit('request-close')" class="btn--close">&times;</button>
        </header>
        <div>
          <slot></slot>
        </div>
      </aside>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Modal',
  props: ['open', 'title', 'modalClass'],
  data() {
    return {
      clickValid: true
    }
  },
  methods: {
    /**
     * This method and #onEndClick() track whether the mouse was
     * down and up on the correct target; if this is not checked
     * for, we can e.g. drag off the modal onto the overlay, and
     * end up accidentally closing the modal when we release
     */
    onBeginClick(e) {
      // Reset click validity
      this.clickValid = true;

      if (e.target !== this.$refs.modalContainer) {
        this.clickValid = false;
      }
    },
    /**
     * See #onBeginClick()
     */
    onEndClick(e) {
      if (e.target !== this.$refs.modalContainer) {
        this.clickValid = false;
      }
    },
    onClickContainer(e) {
      if (e.target === this.$refs.modalContainer
          && this.clickValid) {
        this.$emit('request-close');
      }
    }
  }
}
</script>

<style>
.modal-container {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;

  background: rgba(0, 0, 0, 0.5);

  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  background: white;
}

.modal > header {
  display: flex;
  align-items: center;
  place-content: space-between;
}

.modal header h2 {
  font-size: 1.2em;
  padding: 0;

  margin: 0.8rem;
  margin-right: 0;
}

.modal header .btn--close {
  background: none;
  border: none;
  color: #999;
  
  font-size: 1.3em;
  padding: 0.8rem;
  margin: 0;

  line-height: 0.7em;

  cursor: pointer;
}

.modal > div {
  padding: 0.8rem;
}

.modal-anim-enter {
  opacity: 0;
}

.modal-anim-enter .modal {
  transform: translateY(50%);
}

.modal-anim-enter-active {
  transition: opacity 0.15s ease-in-out;
}

.modal-anim-enter-active .modal {
  transition: transform 0.15s ease-in-out;
}

.modal-anim-leave-active {
  transition: all 0.15s ease-in-out;
}

.modal-anim-leave-to {
  opacity: 0;
}
</style>
