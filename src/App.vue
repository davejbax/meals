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
          />
        </li>
      </ul>
    </section>

    <aside class="grid__sidebar">
      TODO
    </aside>

  </div>
</template>

<script>
import Meal from './components/Meal.vue'

export default {
  name: 'app',
  components: {
    Meal
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
</style>
