<template>
  <div :class="'meal-container card ' + (draggingOver ? 'dragging-over' : '')">
    <Container
      class="drop-zone"
      behaviour="drop-zone"
      group-name="g"
      @drop="onDrop"
      @drag-enter="onDragEnter"
      @drag-leave="onDragLeave"
    >
    </Container>
    <div>
      <h5 class="card__title inline">{{ meal.name }}</h5>
      <span class="card__subtitle inline">{{ totalEnergy }}</span>
    </div>
    <table class="meal">
      <thead>
        <tr>
          <th>Food</th>
          <th>Energy (kcal)</th>
          <th>Carbohydrates</th>
          <th>Protein</th>
          <th>Fat</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in items"
          v-bind:key="index"
        >
          <td>{{ item.food.name }}</td>
          <td>{{ item.quantity * item.food.nutrition.energy }}</td>
          <td>{{ item.quantity * item.food.nutrition.carbs }}</td>
          <td>{{ item.quantity * item.food.nutrition.protein }}</td>
          <td>{{ item.quantity * item.food.nutrition.fat }}</td>
          <td>
            <button class="round-btn" @click="() => onIncreaseQuantity(item)">&plus;</button>
            {{ item.quantity }}
            <button class="round-btn" @click="() => onDecreaseQuantity(item)">&minus;</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { Container } from 'vue-smooth-dnd';

export default {
  name: 'Meal',
  props: ['meal', 'items'],
  components: {
    Container
  },
  data() {
    return {
      draggingOver: false
    }
  },
  computed: {
    totalEnergy() {
      return this.items.reduce((acc, cur) => acc + cur.quantity * cur.food.nutrition.energy, 0);
    }
  },
  methods: {
    onDragEnter: function() {
      this.draggingOver = true;
    },
    onDragLeave: function() {
      this.draggingOver = false;
    },
    onDrop: function(dropResult) {
      this.draggingOver = false;
      
      if (dropResult.addedIndex !== null) {
        this.$emit('add-item', this.meal.id, dropResult.payload);
      }
    },
    onIncreaseQuantity: function(item) {
      this.$emit('change-item-qty', this.meal.id, item.food.id, item.quantity + 1);
    },
    onDecreaseQuantity: function(item) {
      this.$emit('change-item-qty', this.meal.id, item.food.id, item.quantity - 1);
    }
  }
}
</script>

<style>
.meal-container {
  position: relative;
}

/* Ensure hovering passes to the drop zone element when we're dragging
 * something. If not, the drop zone won't register as being 'dragged over',
 * and we won't be able to drop our object
 */
.smooth-dnd-no-user-select .meal-container .drop-zone {
  pointer-events: all;
}

.meal-container .drop-zone {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  pointer-events: none;
}

.dragging-over .meal {
  outline: 2px dashed #CCC;
}

.meal.animated {
  transition-duration: unset!important;
}

.meal {
  width: 100%;

  padding: 0;
  border-collapse: collapse;
}

.meal thead {
  font-size: 0.9em;
  color: #777;
}

.meal tr {
  height: 48px;
  
  border-bottom: 1px solid #DDD;
}

.meal tbody tr:hover {
  background: #EEE;
}

.meal td,
.meal th {
  padding: 0 16px;
}

.round-btn {
  background: #CCC;
  color: #000; 
  font-weight: 700;
  font-size: 1em;
  
  border: none;
  outline: none;
  border-radius: 50%;
  width: 1.4em;
  height: 1.4em;

  cursor: pointer;
}
</style>
