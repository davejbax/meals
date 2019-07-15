<template>
  <div id="app" class="grid">
    
    <section class="grid__main">
      <ul class="meal-list">
        <li
          v-for="meal in meals"
          v-bind:key="meal.id"
        >
          <Meal
            v-bind:meal="meal"
            v-bind:items="getItems(meal.id)"
            @add-item="onAddItem"
            @change-item-qty="onChangeItemQty"
          />
        </li>
      </ul>
    </section>

    <aside class="grid__sidebar">
      <ul class="food-list">
        <!-- TODO move into separate component -->
        <Container
          orientation="vertical"
          behaviour="copy"
          group-name="g"
          drag-class="dragging"
          :get-child-payload="getFoodPayload"
        >
          <Draggable
            v-for="food in foods"
            v-bind:key="food.id"
          >
            <li>
              <Food
                v-bind:food="food"
              />
            </li>
          </Draggable>
        </Container>
      </ul>
    </aside>

  </div>
</template>

<script>
import { Container, Draggable } from 'vue-smooth-dnd';

import Food from './components/Food.vue';
import Meal from './components/Meal.vue'

export default {
  name: 'app',
  components: {
    Meal,
    Food,
    Container,
    Draggable
  },
  data() {
    return {
      meals: [
        {
          id: 0,
          name: 'Breakfast'
        },
        {
          id: 1,
          name: 'Lunch'
        },
        {
          id: 2,
          name: 'Tea'
        }
      ],

      foods: [
        {
          id: 0,
          name: 'Porridge',
          nutrition: {
            energy: 500,
            protein: 10,
            carbs: 10,
            fat: 10
          },
          servingName: 'bowl'
        }
      ],

      plans: [
        {
          id: 0,
          name: 'Monday',
          items: [
            {
              mealId: 0,
              foodId: 0,
              foodQuantity: 1
            }
          ]
        }
      ]
    }
  },
  methods: {
    getItems(mealId) {
      // TODO: non-const plan ID
      let items = this.plans[0].items
        // Filter to find only items concerning the correct meal
        .filter(item => item.mealId === mealId)

        // Map to an object of { food: Food, quantity: number },
        // for easy processing
        .map(item => {
          return {
            food: this.foods.find(food => food.id === item.foodId),
            quantity: item.foodQuantity
          }
        });
      
      return items;
    },
    getFoodPayload(index) {
      return this.foods[index].id;
    },
    onAddItem(mealId, foodId) {
      // TODO: non-const plan ID
      const plan = this.plans[0];

      // See whether we can find an item for this food in this meal
      const itemIndex = plan.items.findIndex(
        item => foodId === item.foodId && mealId === item.mealId
      );

      // If there's an entry for this food in the meal already, just increase
      // the quantity. Otherwise, add an entry.
      if (itemIndex >= 0) {
        plan.items[itemIndex].foodQuantity++;
      } else {
        plan.items.push({
          mealId: mealId,
          foodId: foodId,
          foodQuantity: 1
        });
      }
    },
    onChangeItemQty(mealId, foodId, quantity) {
      const plan = this.plans[0];

      // See whether we can find an item for this food in this meal
      const itemIndex = plan.items.findIndex(
        item => foodId === item.foodId && mealId === item.mealId
      );

      // Stop if we failed to find the item (which shouldn't happen!)
      if (itemIndex < 0) {
        return;
      }

      // If quantity is now 0, remove the item.
      // Otherwise, change quantity
      if (quantity === 0) {
        plan.items.splice(itemIndex, 1);
      } else {
        plan.items[itemIndex].foodQuantity = quantity;
      }
    }
  }
}
</script>

<style>
/**
 * App-wide styles
 */

html, body {
  padding: 0;
  margin: 0;
}

body {
  background: #e5e5e5;
  font-family: 'Roboto', Arial, sans-serif;
}

.smooth-dnd-container.vertical > .smooth-dnd-draggable-wrapper {
  overflow: visible;
}

/**
 * Reusable styles
 */

.inline {
  display: inline-block;
}

.card {
  padding: 16px;
  border-radius: 3px;

  background: white;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
}

.card--hoverable {
  position: relative;
  transition: transform 0.1s ease-in-out;
}

.card--hoverable:after {
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.3);
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;

  opacity: 0;
  transition: opacity 0.1s ease-in-out;

  border-radius: 3px;
}

.card--hoverable:active {
  /*box-shadow: 0 2px 3px rgba(0, 0, 0, 0.5);*/
  transform: translateY(-2px);
}

.card--hoverable:hover:after {
  opacity: 1;
}

.card__title {
  padding: 0;
  margin: 0;
  margin-bottom: 16px;

  font-size: 20px;
  font-weight: 500;
}

.card__subtitle {
  color: #0097A7;
  font-weight: 500;
}

.card__subtitle.inline {
  margin-left: 8px;
}

.dragging .card {
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.7);
}

.smooth-dnd-ghost.animated {
  opacity: 0;
}

/**
 * Component-specific styles
 */

.grid {
  display: flex;
}

.grid__main {
  flex: 2;
}

.grid__sidebar {
  flex: 1;
  flex-shrink: 0;
}

.meal-list {
  list-style: none;
  padding: 0;
  margin: 16px;
}

.meal-list li {
  margin-bottom: 16px;
}

.meal-list li:last-child {
  margin-bottom: 0;
}

.food-list {
  list-style: none;
  padding: 0;
  margin: 16px 0;
  margin-right: 16px;
}
</style>
