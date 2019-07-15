<template>
  <div class="card card--hoverable food">
    <span class="left">
      <h5 class="card__title" v-html="food.highlightedName || food.name"></h5>
      <p>
        Carbs {{ food.nutrition.carbs }}g / Protein {{ food.nutrition.protein }}g / Fat {{ food.nutrition.fat }}g
        ({{ food.servingName }})
      </p>
    </span>
    <span class="right">
      <span class="card__subtitle energy">{{ food.nutrition.energy }}</span>
    </span>
  </div>
</template>

<script>
export default {
  name: 'Food',
  props: ['food']
}
</script>

<style>
.food {
  display: flex;
  align-items: center;

  user-select: none;
  font-size: 1rem;
}

.food .left {
  flex: 1;
}

.food .right {
  flex: 0;
}

.food p {
  margin: 0;
  padding: 0;
  font-size: 0.8em;
  color: #666;
}

.food .card__title {
  font-size: 1.2em;
  margin-bottom: 0.4rem;
}

.food .energy {
  float: right;
  font-size: 1.5em;
}

.food mark {
  color: #e61a49;
  background: none;
}
</style>
