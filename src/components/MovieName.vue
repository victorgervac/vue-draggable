<template>
<!--draggable board item -->
<div class="indi-name">{{ superhero.name }}</div>
</template>
<script>
const SUPERHERO_KEYS = [
  'id',
  'name',
];
export default {
  name: 'MovieName',
  props: {
    superhero:
      {
        type: Object,
        required: true,
        validator(obj) {
          const propKeys = Object.keys(obj);
          return SUPERHERO_KEYS.every((val) => propKeys.includes(val));
        },
      },
  },
};
</script>
<style scooped>
/* .indi-name{
 border: 2px solid #526070;
   padding: 1rem .75rem;
   border-color: #D6D6D6;
   border-style:solid;
   background-color: #F5F5F5;
   font-size: 1rem;
   outline: none;
   border-radius: .5rem;
   width: 100%;
   overflow-y: hidden;
   box-sizing: border-box;

} */
</style>
   <!-- padding: .5em;
    background-color: #EBECF1;
    margin: 1rem;
    width: 100%;
    overflow: hidden;
    color:blue;
    box-sizing: border-box;
    overflow-y: hidden; -->
