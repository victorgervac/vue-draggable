/* eslint-disable no-unused-vars */
<template>
<div>
  <h1>Rate Your Hero</h1>
    <DraggableBoard
      :items="list1"
      name="Your Rate"
      @log="log($event)"
      emptyMessage="Drop Here"
    />
    <DraggableBoard
      :items="list2"
      name="Choices" @log="log($event)"
      emptyMessage="No More options"
     />
  </div>
</template>
<script>

// import draggable from 'vuedraggable';
// import MovieName from './MovieName.vue';
import DraggableBoard from './DraggableBoard.vue';

export default {
  name: 'TwoDraggableExample',
  // display: 'Two Lists',
  // order: 1,
  components: {
    // draggable,
    // MovieName,
    DraggableBoard,
  },
  data() {
    return {
      list1: [
      ],
      list2: [
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
    setItems(key, item) {
      const stringified = JSON.stringify(item);
      localStorage.setItem(key, stringified);
    },
    getItems(key) {
      return JSON.parse(localStorage.getItem(key));
    },
    logAdded(board, item) {
      console.log('added', board, item);
      const boardItems = [item, ...this.getItems(board)];
      this.setItems(board, boardItems);
      // const items = [item, this.getItem('boardName')]
      // then set item
      // - replace items in local storage
      // add item to approprate list
    },
    logRemoved(board, item) {
      console.log('removed', board, item);
      const boardItems = this.getItems(board).filter((c) => c.name !== item.name);
      this.setItems(board, boardItems);
      debugger;
      // const items = this.getItem('boardName').filter(c => c.name != item.name)
      // save item to local storage
      // add item to approprate list
    },
    log(evt) {
      // check the type of log
      const isRemoved = Object.keys(evt).includes('removed');
      const isAdded = Object.keys(evt).includes('added');
      if (isRemoved) this.logRemoved(evt.board, evt.removed.element);
      if (isAdded) this.logAdded(evt.board, evt.added.element);

      // call method per log type aka added, removed  & passs in the board + data

      // console.log('two drggable example log', evt, isRemoved, isAdded);
    },
  },
  mounted() {
    // testing stuff change it later
    const defaultItems2 = [{ name: 'Clarkson', id: 5 },
      { name: 'Peter Parker', id: 6 },
      { name: 'Bruce Wayne', id: 7 }];
    this.setItems('list2', defaultItems2);
    const defaultItems1 = [];
    this.setItems('list1', defaultItems1);
    // getitems
    this.list1 = this.getItems('list1');
    this.list2 = this.getItems('list2');
  },
};
</script>
<style>
  /* .full-card{
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

  } */
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
