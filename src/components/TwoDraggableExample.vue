<template>
  <h1>Rate Your Hero</h1>
  <div class="draging-message">{{draggingAction}}</div>
  <div class="full-card">
    <div class="rated-card">
      <h3 class="card-tittle">Your Ratting</h3>
      <draggable
        class="list-group"
        :list="list1"
        group="people"
        @change="log"
        itemKey="name"
        @start="dragging = true"
        @end="dragging = false"
      >
      <template  #header>
      <div v-if="!list1.length" class="empty-square">Drop Here</div>
      </template>
   <template #item="{ element, index }">
          <div class="single-option">{{ element.name }} {{ ++index }}</div>
        </template>
          </draggable>
    </div>

    <div class="choices-card">
      <h3 class="card-tittle">Choices</h3>
      <draggable
        class="list-group"
        :list="list2"
        group="people"
        @change="log"
        itemKey="name"
        @start="dragging = true"
        @end="dragging = false"
      >
         <template #footer>
     <p v-if="!list2.length" class="empty-square">No Options</p>
  </template>
        <template #item="{ element}">
        <div class="single-option">
        <MovieName :superhero="element"
        :class="list-group-item"/>
        </div>

        </template>
      </draggable>
    </div>
    <!-- <rawDisplayer class="col-3" :value="list1" title="List 1" /> -->
    <!-- <rawDisplayer class="col-3" :value="list2" title="List 2" /> -->
  </div>
</template>
<script>

import draggable from 'vuedraggable';
import MovieName from './MovieName.vue';

export default {
  name: 'TwoDraggableExample',
  // display: 'Two Lists',
  // order: 1,
  components: {
    draggable,
    MovieName,
  },
  data() {
    return {
      list1: [
      ],
      list2: [
        { name: 'Clarkson', id: 5 },
        { name: 'Peter Parker', id: 6 },
        { name: 'Bruce Wayne', id: 7 },
      ],
      dragging: false,
    };
  },
  computed: {
    draggingAction() {
      return this.dragging ? 'Draging' : '';
    },
  },
  methods: {
    setItem(key, item) {
      const stringified = JSON.stringify(item);
      localStorage.setItem(key, stringified);
    },
    getItem(key) {
      return JSON.parse(localStorage.getItem(key));
    },
    watch: {
      list2(newSuperhero) {
        localStorage.superhero = newSuperhero;
      },
      list1(newSuperhero) {
        localStorage.superhero = newSuperhero;
      },
    },
    add() {
      console.log('name moved');
      // this.list.push({ name: 'Juan' });
    },
    replace() {
      this.list = [{ name: 'Edgard' }];
    },
    clone(el) {
      return {
        name: `${el.name} cloned`,
      };
    },
    log(evt) {
      window.console.log(evt);
    },
  },
  mounted() {
  },
};
</script>
<style>
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
/* .list-group{
    border: 2px solid #526070;
    padding: .5em;
    background-color: #EBECF1;
    margin: 1rem;
    overflow: hidden;
    box-sizing: border-box;
} */
/* .row-two{
  display: flex;
  justify-content: space-around;
} */
/* .col-choices{
  background-color: aqua;
  box-sizing: border-box;
} */
</style>
