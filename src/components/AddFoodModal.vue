<template>
  <Modal
    title="Add new food"
    modal-class="modal-add-food"
    :open="open"
    @request-close="() => this.$emit('request-close')"
  >
    <form 
      name="add-food"
      autocomplete="off"
      method="dialog"
      @submit="onSubmit"
    >
      <FormField
        name="food-name"
        placeholder="Name"
        class="modal-add-food__field"
        required
        @input="food.name = $event.target.value"
      />
      <FormField
        name="food-desc"
        placeholder="Description"
        type="multiline"
        class="modal-add-food__field"
        @input="food.description = $event.target.value"
      />
      <div class="modal-add-food__row modal-add-food__row--2-1">
        <FormField
          name="food-serving-name"
          placeholder="Serving name"
          class="modal-add-food__field"
          @input="food.servingName = $event.target.value"
        />
        <FormField
          name="food-serving-weight"
          placeholder="Serving weight (g)"
          type="number"
          class="modal-add-food__field"
          required
          @input="food.servingWeight = $event.target.value"
        />
      </div>
      <h4 class="modal-add-food__nutrition-label">Nutrition per 100g</h4>
      <div class="modal-add-food__row">
        <FormField
          name="food-energy"
          placeholder="Energy (kcal)"
          type="number"
          class="modal-add-food__field modal-add-food__field--small"
          required
          @input="food.nutrition.energy = $event.target.value"
        />
        <FormField
          name="food-carbs"
          placeholder="Carbohydrates (g)"
          type="number"
          class="modal-add-food__field modal-add-food__field--small"
          required
          @input="food.nutrition.carbs = $event.target.value"
        />
      </div>
      <div class="modal-add-food__row">
        <FormField
          name="food-protein"
          placeholder="Protein (g)"
          type="number"
          class="modal-add-food__field modal-add-food__field--small"
          required
          @input="food.nutrition.protein = $event.target.value"
        />
        <FormField
          name="food-fat"
          placeholder="Fat (g)"
          type="number"
          class="modal-add-food__field modal-add-food__field--small"
          required
          @input="food.nutrition.fat = $event.target.value"
        />
      </div>
      <footer style="text-align: right">
        <button class="btn" type="submit">Add food</button>
      </footer>
    </form>
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
  },
  methods: {
    onSubmit() {
      this.$emit('submit', this.food);
    }
  },
  data() {
    return {
      food: {
        id: null,
        name: null,
        description: null,
        servingName: null,
        nutrition: {
          energy: null,
          carbs: null,
          fat: null,
          protein: null
        }
      }
    }
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

.modal-add-food__row--2-1 > *:first-child {
  flex: 2;
}

.modal-add-food__row--2-1 > *:last-child {
  flex: 1;
}

.modal-add-food__nutrition-label {
  font-weight: 500;
  margin: 0.8rem 0;
}
</style>
