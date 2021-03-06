<template>
  <div id="app" class="grid">
    
    <section class="grid__main">
      <ul class="meal-list">
        <li
          v-for="meal in meals"
          :key="meal.id"
        >
          <Meal
            :meal="meal"
            :items="getMealItems(meal.id)"
            @add-item="onAddItem"
            @change-item-qty="onChangeItemQty"
          />
        </li>
      </ul>
    </section>

    <aside class="grid__sidebar">
      <FoodList :foods="foods" />
    </aside>

    <FloatingActionButton @click="onOpenAddFoodModal">&plus;</FloatingActionButton>

    <AddFoodModal
      :open="addFoodModalOpen"
      @request-close="onCloseAddFoodModal"
      @submit="onSubmitAddFoodModal"
    />

  </div>
</template>

<script>
import AddFoodModal from './components/AddFoodModal.vue';
import FloatingActionButton from './components/FloatingActionButton.vue';
import FoodList from './components/FoodList.vue';
import Meal from './components/Meal.vue'

export default {
  name: 'app',
  components: {
    Meal,
    AddFoodModal,
    FoodList,
    FloatingActionButton
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
      ],

      addFoodModalOpen: false
    }
  },
  methods: {
    getMealItems(mealId) {
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
    },
    onOpenAddFoodModal() {
      this.addFoodModalOpen = true;
    },
    onCloseAddFoodModal() {
      this.addFoodModalOpen = false;
    },
    onSubmitAddFoodModal(food) {
      this.addFoodModalOpen = false;
      
      // Create new ID of max ID + 1
      const newId = this.foods.reduce((acc, cur) => cur > acc ? cur : acc) + 1;
      food.id = newId;

      // Add to foods list
      this.foods.push(food);
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

html {
  font-size: 20px;
}

/* Scale down font for smaller devices */
@media screen and (max-width: 1024px){
  html { font-size: 15px; }
}

body {
  background: #e5e5e5;
  font-family: 'Roboto', Arial, sans-serif;
}

button, input {
  font-family: 'Roboto', Arial, sans-serif;
}

/**
 * Reusable styles
 */

.inline {
  display: inline-block;
}

.card {
  padding: 0.8rem;
  border-radius: 0.15rem;

  background: white;
  box-shadow: 0 0.05rem 0.15rem rgba(0, 0, 0, 0.5);
}

.card--hoverable {
  position: relative;
  transition: transform 0.1s ease-in-out;
}

.card--hoverable:active {
  transform: translateY(-0.1rem);
}

/* Use a pseudo-element to animate box-shadow through opacity */
.card--hoverable:after {
  box-shadow: 0 0.15rem 0.25rem rgba(0, 0, 0, 0.3);
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;

  opacity: 0;
  transition: opacity 0.1s ease-in-out;

  border-radius: 0.15rem;
}

.card--hoverable:hover:after {
  opacity: 1;
}

.card__title {
  padding: 0;
  margin: 0;
  margin-bottom: 0.8rem;

  font-size: 1rem;
  font-weight: 500;
}

.card__subtitle {
  color: #0097A7;
  font-weight: 500;
}

.card__subtitle.inline {
  margin-left: 0.4rem;
}

.btn {
  position: relative;
  overflow: hidden;

  background: #0097A7;
  color: white;

  border: none;
  border-radius: 3px;
  padding: 0.8rem 1rem;

  font-size: 0.8rem;
  font-weight: 500;
  text-transform: uppercase;

  cursor: pointer;

  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);

  transition: background 0.1s ease-in-out;
}

.btn:hover {
  background: #14a7b7
}

.btn:focus {
  background: #47bdca;
  outline: none;
}

/* Ripple effect */
.btn:after {
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

.btn:active:after {
  transform: scale(0);
  opacity: 0.3;
  transition: 0s;
}

.btn--secondary {
  background: none;
  color: #666;

  box-shadow: inset 0 0 1px #ccc;
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
  margin: 0.8rem;
}

.meal-list li {
  margin-bottom: 0.8rem;
}

.meal-list li:last-child {
  margin-bottom: 0;
}
</style>
