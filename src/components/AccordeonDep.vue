<template>
  <div class="ui-ctn">
    <button @click="$emit('statebio')">bio{{state.bio ? '[x]' : '[_]'}}</button>

    <button class="button-parent" @click="$emit('stateImage')">images{{state.tel ? '[x]' : '[_]'}}</button>
    <div class="button-ctn-plusMoins">
    <button class="button-plusMoins" @click="$emit('changeimg', -10)">+</button>
    <button class="button-plusMoins button-closing" @click="$emit('changeimg', +10)">-</button>
</div>
    <button @click="$emit('stateTel')">darkmode{{state.tel ? '[_]' : '[x]'}}</button>
    <button @click="$emit('stateTel')">projects{{state.tel ? '[_]' : '[x]'}}</button>
    <button @click="$emit('stateTel')">journal{{state.tel ? '[_]' : '[x]'}}</button>
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
.button-plusMoins {
  margin-right: 0;
  margin-left:0;
  margin-top: 0;
  width: 40px;
  border-left: none;
  height: 20px;
  display: block;
  line-height: 0;
}
.button-closing {
  border-top: none;
  margin-right: 10px;
  margin-top: 0;
}
.button-parent {
  float:left;
  margin-right: 0;
}
button, .button-parent {
  font-size: 16px;
  border: 1px solid white;
  color: white;
  background: none;
  font-family: 'IBM Plex Mono', monospace;
}
button {
  margin-right: 10px;

}

.button-ctn-plusMoins {
  margin-top:0 ;

}

.button-ctn-plusMoins, button {
  margin-top: 10px;
  height: 40px;
  
}

.ui-ctn {
  flex-wrap: wrap;
  box-sizing: border-box;
  display: flex;
  top : 8px;
  position: sticky;
  width:calc(100% + 20px);
  height: fit-content;
  background-color: black;
  padding-left: 10px;
  padding-right: 10px;

  overflow: scroll;
  margin-top: 0px;
  z-index: 6969696969;
}
</style>