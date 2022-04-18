<template>
  <div class="row">
    <div class="col-2">
      <div class="form-group">
        <div
          class="btn-group-vertical buttons"
          role="group"
          aria-label="Basic example"
        >
          <button class="btn btn-secondary" @click="add">Add</button>
          <button class="btn btn-secondary" @click="replace">Replace</button>
          <button class="btn btn-secondary" @click="sort">Reset</button>
        </div>

        <!-- <div class="form-check">
          <input
            id="disabled"
            type="checkbox"
            v-model="enabled"
            class="form-check-input"
          />
            <label class="form-check-label" for="disabled">DnD enabled</label>
        </div> -->
      </div>
    </div>

    <div class="col-6">
      <h3>{{ draggingInfo }}</h3>

      <draggable
        :list="movies"
        :disabled="!enabled"
        item-key="name"
        class="list-group"
        ghost-class="ghost"
        :move="checkMove"
        @start="dragging = true"
        @end="dragging = false"
      >
        <template #item="{ element }">
         <MovieName :superhero="element"
        class="list-group-item"/>
        </template>
      </draggable>
    </div>
    <div>
    </div>
    <!-- <rawDisplayer class="col-3" :value="list" title="List" /> -->
  </div>
</template>

<script>
import draggable from 'vuedraggable';
import MovieName from './MovieName.vue';

// const newName = nameList;
const id = 1;
export default {
  name: 'VueDaggrableExample',
  display: 'Simple',
  order: 0,
  components: {
    draggable,
    MovieName,

  },
  data() {
    return {
      enabled: true,
      movies: [
        { name: 'Batman', id: 0 },
        { name: 'Wonder Woman', id: 1 },
        { name: 'Spiderman', id: 2 },
      ],
      dragging: false,
    };
  },
  computed: {
    draggingInfo() {
      return this.dragging ? `draging ${id}` : 'Start Dragging';
    },
    // newName() {
    //   newmovies = namemovies.value.name;
    // },

  },
  methods: {
    add() {
      const movie = { name: 'yada', id: 0 };
      this.movies = [movie, ...this.movies];
    },
    replace() {
      this.movies = [{ name: 'Edgard' }];
    },
    checkMove(e) {
      window.console.log(`Moving index: ${e.draggedContext.futureIndex}`);
    },

    // sort() {
    //   this.movies = this.movies.sort((a, b) => a.order - b.order);
    // },
  },
};
</script>
<style scoped>
.buttons {
  margin-top: 35px;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.not-draggable {
  cursor: no-drop;
  border: 1px solid red;
}
/* .list-group-item{
    border: 2px solid #526070;
    padding: .5em;
    background-color: #EBECF1;
    margin: 1rem;
    overflow: hidden;
    box-sizing: border-box;
} */
</style>
