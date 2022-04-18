<template>
  <div class="choices-card">
    <h3 class="card-tittle">{{name}}</h3>
    <draggable
      class="list-group"
      :list="items"
      group="people"
      @change="log"
      itemKey="name"
      @start="dragging = true"
      @end="dragging = false"
    >
      <template #footer>
        <p v-if="!items.length" class="empty-square">{{emptyMessage}}</p>
      </template>
      <template #item="{ element}">
        <div class="single-option">

          <MovieName :superhero="element" />
        </div>
      </template>
    </draggable>
  </div>
</template>
<script>
import draggable from 'vuedraggable';
import MovieName from './MovieName.vue';

const BOARD_KEYS = [
  'id',
  'name',
];
export default {
  name: 'DraggableBoard',
  components: {
    draggable,
    MovieName,
  },
  props: {
    items: {
      type: Array,
      default() {
        return [];
      },
      validator(arr) {
        return arr
          .map((c) => Object.keys(c)) // map over arr to get keys that were used in each object
          .every((propKeys) => BOARD_KEYS // loop over every array of keys to return true
            .every((val) => propKeys.includes(val))); // all of the keys must include the board keys
      },
    },
    name: {
      type: String,
      required: true,
    },
    emptyMessage: {
      type: String,
      default: 'Empty',
    },
  },
  methods: {
    add() {
      console.log('name moved');
      // this.list.push({ name: 'Juan' });
    },
    replace() {
      //
    },
    clone(el) {
      return {
        name: `${el.name} cloned`,
      };
    },
    log(evt) {
      // emit log event
      this.$emit('log', { ...evt, board: this.name });
    },
  },
};

</script>
<style scoped>
.full-card{
    background-color: #EBECF0;
    display: flex;
    justify-content: space-around;
    border-radius: 3px;
  }
  .rated-card{
      background-color: white;
      color:black;
      padding: 1rem;
      border-radius: 3px;
      margin: 1rem;
  }
  .choices-card{
    background-color: white;
    color: black;
    padding: 1rem;
    border-radius: 3px;
    margin: 1rem;
  }
  .single-option{
      background-color: #EBECF0;
      color:black;
      margin:1rem;
      padding:1rem;
      border-radius: 3px;
      box-shadow:2px 2px 2px 1px gray;
  }
  .empty-square{
    padding: 1rem;
    border: dotted;
    opacity: 0.5;
    background-color: white;
    border-radius: 5px;
  }
  .draging-message{
    color: red;
    font-weight: bold;

  }
</style>
