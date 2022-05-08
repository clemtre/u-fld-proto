<template>
  <div class="ui-ctn">
    <button @click="$emit('stateBio')">bio{{state.bio ? '[x]' : '[_]'}}</button>
    <button @click="$emit('stateTel')">images{{state.tel ? '[x]' : '[_]'}}</button>
    <!-- <button><star-glyph></star-glyph></button> -->
    <!-- <p v-show="state.bio">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Suscipit nam rem quas corrupti, dolore, nobis iure magnam, voluptatem rerum explicabo esse. Odio ipsum quibusdam voluptas, inventore iusto dignissimos maiores corporis.
    Aperiam consectetur soluta deleniti ullam esse. Velit eius unde, ipsa alias molestias eveniet ratione consectetur ducimus id dolorum minus laboriosam cumque nesciunt accusantium quo corporis earum eos eum autem necessitatibus.
    Sequi obcaecati aperiam illo dolor doloribus ipsum, nam molestias vel impedit voluptatum quos. Optio illo repellendus, eveniet nobis minima amet autem blanditiis incidunt iusto deserunt, est aut id a accusantium.</p>


    <p style="color:red" v-show="state.tel">Lorem ipsum dolor sit amet, la révolution</p> -->
  
  </div>
</template>

<script>
// import StarGlyph from './StarGlyph.vue';

export default {
  name: "AccordeonDep",
  // components:{ StarGlyph },
 props: ['state'],
};
</script>


<style>

button:hover {
  background: fuchsia;
  color: white;
  text-decoration: underline;
  cursor: pointer;
  opacity: 1;
}

button {
  font-size: 16px;
  border: 1px solid white;
  color: white;
  background: none;
  margin-right: 10px;
  font-family: 'IBM Plex Mono', monospace;
}

.ui-ctn {
  display: flex;
  top : 8px;
  position: sticky;
  width: 100%;
  height: fit-content;
  background-color: black;
  padding: 10px;
  margin-top: 0px;
  z-index: 6969696969;
}
</style>