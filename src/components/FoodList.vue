<template>
  <div class="food-list-container">
    <div class="search">
      <svg class="search__icon" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 640 640" width="48" height="48"><defs><path d="M281.32.86l10.49 1.07 10.36 1.47 10.23 1.88 10.08 2.28 9.93 2.66 9.77 3.03 9.6 3.41 9.42 3.77 9.24 4.12 9.04 4.47 8.85 4.8 8.63 5.13 8.41 5.45 8.18 5.76 7.95 6.07 7.71 6.36 7.45 6.64 7.19 6.92 6.92 7.19 6.64 7.45 6.36 7.71 6.07 7.95 5.76 8.18 5.45 8.41 5.13 8.63 4.8 8.85 4.47 9.04 4.12 9.24 3.77 9.42 3.41 9.6 3.03 9.77 2.66 9.93 2.28 10.08 1.88 10.23 1.47 10.36 1.07 10.49.64 10.6L520 260l-.22 10.72-.64 10.6-1.07 10.49-1.47 10.36-1.88 10.23-2.28 10.08-2.66 9.93-3.03 9.77-3.41 9.6-3.77 9.42-4.12 9.24-4.47 9.04-4.8 8.85-5.13 8.63-5.26 8.12L640 569.29 569.29 640 405.08 475.79l-8.12 5.26-8.63 5.13-8.85 4.8-9.04 4.47-9.24 4.12-9.42 3.77-9.6 3.41-9.77 3.03-9.93 2.66-10.08 2.28-10.23 1.88-10.36 1.47-10.49 1.07-10.6.64L260 520l-10.72-.22-10.6-.64-10.49-1.07-10.36-1.47-10.23-1.88-10.08-2.28-9.93-2.66-9.77-3.03-9.6-3.41-9.42-3.77-9.24-4.12-9.04-4.47-8.85-4.8-8.63-5.13-8.41-5.45-8.18-5.76-7.95-6.07-7.71-6.36-7.45-6.64-7.19-6.92-6.92-7.19-6.64-7.45-6.36-7.71-6.07-7.95-5.76-8.18-5.45-8.41-5.13-8.63-4.8-8.85-4.47-9.04-4.12-9.24-3.77-9.42-3.41-9.6-3.03-9.77-2.66-9.93-2.28-10.08-1.88-10.23-1.47-10.36-1.07-10.49-.64-10.6L0 260l.22-10.72.64-10.6 1.07-10.49 1.47-10.36 1.88-10.23 2.28-10.08 2.66-9.93 3.03-9.77 3.41-9.6 3.77-9.42 4.12-9.24 4.47-9.04 4.8-8.85 5.13-8.63 5.45-8.41 5.76-8.18 6.07-7.95 6.36-7.71 6.64-7.45 6.92-7.19 7.19-6.92 7.45-6.64 7.71-6.36 7.95-6.07 8.18-5.76 8.41-5.45 8.63-5.13 8.85-4.8 9.04-4.47 9.24-4.12 9.42-3.77 9.6-3.41 9.77-3.03 9.93-2.66 10.08-2.28 10.23-1.88 10.36-1.47L238.68.86l10.6-.64L260 0l10.72.22 10.6.64zm-34.48 99.25l-6.47.65-6.39.91-6.31 1.16-6.22 1.41-6.13 1.64-6.03 1.87-5.92 2.11-5.81 2.32-5.7 2.54-5.58 2.76-5.46 2.96-5.33 3.17-5.19 3.36-5.05 3.56-4.9 3.74-4.75 3.92-4.6 4.1-4.44 4.27-4.27 4.44-4.1 4.6-3.92 4.75-3.74 4.9-3.56 5.05-3.36 5.19-3.17 5.33-2.96 5.46-2.76 5.58-2.54 5.7-2.32 5.81-2.11 5.92-1.87 6.03-1.64 6.13-1.41 6.22-1.16 6.31-.91 6.39-.65 6.47-.4 6.55-.14 6.61.14 6.61.4 6.55.65 6.47.91 6.39 1.16 6.31 1.41 6.22 1.64 6.13 1.87 6.03 2.11 5.92 2.32 5.81 2.54 5.7 2.76 5.58 2.96 5.46 3.17 5.33 3.36 5.19 3.56 5.05 3.74 4.9 3.92 4.75 4.1 4.6 4.27 4.44 4.44 4.27 4.6 4.1 4.75 3.92 4.9 3.74 5.05 3.56 5.19 3.36 5.33 3.17 5.46 2.96 5.58 2.76 5.7 2.54 5.81 2.32 5.92 2.11 6.03 1.87 6.13 1.64 6.22 1.41 6.31 1.16 6.39.91 6.47.65 6.55.4 6.61.14 6.61-.14 6.55-.4 6.47-.65 6.39-.91 6.31-1.16 6.22-1.41 6.13-1.64 6.03-1.87 5.92-2.11 5.81-2.32 5.7-2.54 5.58-2.76 5.46-2.96 5.33-3.17 5.19-3.36 5.05-3.56 4.9-3.74 4.75-3.92 4.6-4.1 4.44-4.27 4.27-4.44 4.1-4.6 3.92-4.75 3.74-4.9 3.56-5.05 3.36-5.19 3.17-5.33 2.96-5.46 2.76-5.58 2.54-5.7 2.32-5.81 2.11-5.92 1.87-6.03 1.64-6.13 1.41-6.22 1.16-6.31.91-6.39.65-6.47.4-6.55.14-6.61-.14-6.61-.4-6.55-.65-6.47-.91-6.39-1.16-6.31-1.41-6.22-1.64-6.13-1.87-6.03-2.11-5.92-2.32-5.81-2.54-5.7-2.76-5.58-2.96-5.46-3.17-5.33-3.36-5.19-3.56-5.05-3.74-4.9-3.92-4.75-4.1-4.6-4.27-4.44-4.44-4.27-4.6-4.1-4.75-3.92-4.9-3.74-5.05-3.56-5.19-3.36-5.33-3.17-5.46-2.96-5.58-2.76-5.7-2.54-5.81-2.32-5.92-2.11-6.03-1.87-6.13-1.64-6.22-1.41-6.31-1.16-6.39-.91-6.47-.65-6.55-.4-6.61-.14-6.61.14-6.55.4z" id="a"/></defs><use xlink:href="#a"/></svg>
      <input
        class="search__box"
        type="text"
        name="query"
        autofocus
        v-model="query"
        ref="query"
      />
    </div>
    <ul class="food-list">
      <Container
        orientation="vertical"
        behaviour="copy"
        group-name="meal-drop"
        drag-class="dragging"
        :get-child-payload="getFoodPayload"
      >
        <Draggable
          v-for="food in filteredFoods"
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
  </div>
</template>

<script>
import { Container, Draggable } from 'vue-smooth-dnd';
import Fuse from 'fuse.js';
import Food from './Food.vue';

const FUSE_OPTIONS = {
  keys: ['name'],
  includeMatches: true
};

function insertString(str, index, insert) {
  return str.slice(0, index) + insert + str.slice(index);
}

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
  data: function() {
    return {
      query: '',
      fuse: new Fuse(
        this.foods,
        FUSE_OPTIONS
      )
    }
  },
  mounted() {
    document.body.addEventListener('keydown', this.onBodyKeyDown);
  },
  beforeDestroy() {
    document.body.removeEventListener('keydown', this.onBodyKeyDown);
  },
  methods: {
    getFoodPayload(index) {
      return this.foods[index].id;
    },
    onBodyKeyDown(event) {
      if (document.activeElement === document.body
          && event.key.match(/[a-zA-Z0-9]/)) {
        // TODO: ensure modal isn't open
        this.query = '';
        this.$refs.query.focus();
      }
    }
  },
  computed: {
    filteredFoods: function() {
      if (!this.fuse || this.query.length === 0) {
        return this.foods;
      } else {
        const results = this.fuse.search(this.query);
        
        return results.map(result => {
          // We only get the first 'match', since we're only
          // searching by a single key.
          const match = result.matches[0];

          const highlightStart = '<mark>';
          const highlightEnd = '</mark>';
          let highlighted = match.value;
          let addedChars = 0;
          for (let indexPair of match.indices) {
            // Insert highlight start
            highlighted = insertString(
              highlighted,
              indexPair[0] + addedChars,
              highlightStart  
            );
            addedChars += highlightStart.length;

            // Insert highlight end
            highlighted = insertString(
              highlighted,
              indexPair[1] + 1 + addedChars, // End index is inclusive
              highlightEnd
            );
            addedChars += highlightEnd.length;
          }

          const newResult = { ...result.item, highlightedName: highlighted };
          return newResult;

        });
      }
    }
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

.food-list-container {
  margin: 0.8rem;
  margin-left: 0;
}

.food-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.search {
  margin-bottom: 0.8rem;

  display: flex;
  align-items: center;
}

.search__icon {
  width: 1rem;
  height: 1rem;

  flex: 0;
  flex-basis: auto;
}

.search__box {
  background: none;
  border: none;
  border-bottom: 3px solid #666;

  font-size: 1rem;
  padding: 0.5em;
  margin-left: 0.4rem;

  flex: 1;
}

.search__box:focus {
  outline: none;
  border-bottom: 3px solid #0097a7;
}
</style>
