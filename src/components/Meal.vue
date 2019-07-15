<template>
  <div class="card">
    <div>
      <h5 class="card__title inline">{{ meal.name }}</h5>
      <span class="card__subtitle inline">500</span>
    </div>
    <table class="meal">
      <thead>
        <tr>
          <th></th>
          <th>Food</th>
          <th>Energy (kcal)</th>
          <th>Carbohydrates</th>
          <th>Protein</th>
          <th>Fat</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in items"
          v-bind:key="index"
        >
          <td>{{ item.quantity }}</td>
          <td>{{ item.food.name }}</td>
          <td>{{ item.quantity * item.food.nutrition.energy }}</td>
          <td>{{ item.quantity * item.food.nutrition.carbs }}</td>
          <td>{{ item.quantity * item.food.nutrition.protein }}</td>
          <td>{{ item.quantity * item.food.nutrition.fat }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'Meal',
  props: ['meal', 'items']
}
</script>

<style>
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
</style>
