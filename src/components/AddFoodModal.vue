<template>
  <Modal
    title="Add new food"
    modal-class="modal-add-food"
    :open="open"
    @request-close="() => this.$emit('request-close')"
  >
    <FormField
      name="food-name"
      placeholder="Name"
      class="modal-add-food__field"
    />
    <FormField
      name="food-desc"
      placeholder="Description"
      class="modal-add-food__field"
    />
    <FormField
      name="food-serving-name"
      placeholder="Serving name"
      class="modal-add-food__field"
    />
    <div class="modal-add-food__row">
      <FormField
        name="food-energy"
        placeholder="Energy (kcal)"
        class="modal-add-food__field modal-add-food__field--small"
      />
      <FormField
        name="food-carbs"
        placeholder="Carbohydrates (g)"
        class="modal-add-food__field modal-add-food__field--small"
      />
    </div>
    <div class="modal-add-food__row">
      <FormField
        name="food-protein"
        placeholder="Protein (g)"
        class="modal-add-food__field modal-add-food__field--small"
      />
      <FormField
        name="food-fat"
        placeholder="Fat (g)"
        class="modal-add-food__field modal-add-food__field--small"
      />
    </div>
  </Modal>
</template>

<script>
import FormField from './FormField.vue';
import Modal from './Modal.vue';

export default {
  name: 'AddFoodModal',
  props: ['open'],
  components: {
    FormField,
    Modal
  }
}
</script>

<style>
.modal-add-food {
  width: 40rem;
  max-width: 100%;
}

.modal-add-food__field {
  margin-bottom: 0.8rem;
}

.modal-add-food__row {
  display: flex;
}

.modal-add-food__row > * {
  flex-basis: 100%;
}

.modal-add-food__row > *:first-child {
  margin-right: 0.4rem;
}

.modal-add-food__row > *:last-child {
  margin-left: 0.4rem;
}
</style>
