<template>
  <ul class="food-list">
    <Container
      orientation="vertical"
      behaviour="copy"
      group-name="meal-drop"
      drag-class="dragging"
      :get-child-payload="getFoodPayload"
    >
      <Draggable
        v-for="food in foods"
        :key="food.id"
      >
        <li>
          <Food
            :food="food"
          />
        </li>
      </Draggable>
    </Container>
  </ul>
</template>

<script>
import { Container, Draggable } from 'vue-smooth-dnd';
import Food from './Food.vue';

export default {
  name: 'FoodList',
  props: [
    'foods'
  ],
  components: {
    Food,
    Container,
    Draggable
  },
  methods: {
    getFoodPayload(index) {
      return this.foods[index].id;
    },
  }
}
</script>

<style>
/* Fade out ghost element when dropped */
.smooth-dnd-ghost.animated {
  opacity: 0;
}

/* Ensure box-shadows on foods are visible */
.smooth-dnd-container.vertical > .smooth-dnd-draggable-wrapper {
  overflow: visible;
}

/* Increase box-shadow (elevation) when dragging a food (.dragging is drag-class) */
.dragging .food {
  box-shadow: 0 0.15rem 0.4rem rgba(0, 0, 0, 0.7);
}

.food-list {
  list-style: none;
  padding: 0;
  margin: 0.8rem 0;
  margin-right: 0.8rem;
}
</style>
