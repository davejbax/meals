<template>
  <div
    :class="['form-field', focused ? 'focused' : '', value ? 'full' : '']"
    @click="onClickContainer"
  >
    <label :for="name">{{ placeholder }}</label>
    <span class="form-field__content">
      <input
        v-if="'number' === type"

        type="number"
        ref="input"

        v-model="value"
        :name="name"
        :required="required"
        @blur="() => this.focused = false"
        @focus="() => this.focused = true"
        @input="(e) => this.$emit('input', e)"
      />
      <textarea
        v-else-if="'multiline' === type"

        ref="input"

        v-model="value"
        :name="name"
        :required="required"
        @blur="() => this.focused = false"
        @focus="() => this.focused = true"
        @input="(e) => this.$emit('input', e)"
      />
      <input
        v-else

        type="text"
        ref="input"
        
        v-model="value"
        :name="name"
        :required="required"
        @blur="() => this.focused = false"
        @focus="() => this.focused = true"
        @input="(e) => this.$emit('input', e)"
      />
    </span>
  </div>
</template>

<script>
export default {
  name: 'FormField',
  props: {
    name: String,
    placeholder: String,
    type: {
      type: String,
      default: 'text'
    },
    required: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      focused: false,
      value: ''
    }
  },
  methods: {
    onClickContainer() {
      this.$refs.input.focus();
    }
  }
}
</script>

<style>
.form-field {
  background: #ECECEC;
  padding-bottom: 2px;

  position: relative;
}

.form-field:after {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;

  height: 2px;
  content: '';

  background: #666;

  transform-origin: 0 100%;
  transform: scaleY(0.5);
  transition: all 0.1s ease-in-out;
}

.form-field:hover:after,
.form-field.focused:after {
  transform: scaleY(1);
}

.form-field.focused:after {
  background: #0097A7;
}

.form-field > label {
  position: absolute;
  left: 0.6rem;
  top: 50%;

  margin-top: -0.5em;
  line-height: 1em;
  font-size: 0.9rem;

  user-select: none;
  pointer-events: none;

  transform-origin: 0 0;
  transition: all 0.1s ease-in-out;
}

.form-field.focused > label,
.form-field.full > label {
  top: 0.8em;
  margin-top: 0;
  transform: scale(0.8);
}

.form-field.full > label {
  color: #666;
}

.form-field.focused > label,
.form-field.focused.full > label {
  color: #0097A7;
}

.form-field__content {
  display: block;

  padding-top: 1em;
}

.form-field__content > input,
.form-field__content > textarea {
  border: none;
  background: none;

  padding: 0.6rem;
  width: 100%;
  box-sizing: border-box;

  font-size: 0.9rem;
}

.form-field__content > textarea {
  /* Padding on sides for the sake of not overflowing,
   * and bottom so the grip to resize the textarea is
   * in the right place.
   */
  padding: 0 0.6em;
  padding-bottom: 0.6em;

  /* Margin on the top, so we don't cover the label */
  margin-top: 0.6em;

  /* Prevent untracked space on bottom of textarea from
   * appearing, and only allow resizing vertically
   */
  vertical-align: top;
  resize: vertical;

  font-family: Roboto, Arial, sans-serif;
}

.form-field__content > input:focus,
.form-field__content > textarea:focus {
  outline: none;
}
</style>
