<template>
  <div v-bind:style="[ui]">
    <button @click="$emit('statebio')">
      bio{{ state.bio ? "[x]" : "[_]" }}
    </button>

    <button class="button-parent" @click="$emit('stateImages')">
      images{{ state.images ? "[x]" : "[_]" }}
    </button>
    <div v-bind:style="[ctnPlusMoins]" class="button-ctn-plusMoins">
      <button class="button-plusMoins" v-bind:style="{marginRight : 0, borderRight : 'none'}" @click="$emit('changeimg', -10)">
        +
      </button>
      <button
        class="button-plusMoins button-closing"
        @click="$emit('changeimg', 10)"
      >
        -
      </button>
    </div>
    <button @click="$emit('stateTel')">
      darkmode{{ state.tel ? "[_]" : "[x]" }}
    </button>
    <button @click="$emit('stateTel')">
      projects{{ state.tel ? "[_]" : "[x]" }}
    </button>
    <button @click="$emit('stateTel')">
      journal{{ state.tel ? "[_]" : "[x]" }}
    </button>
  </div>
</template>

<script>
// import StarGlyph from './StarGlyph.vue';

export default {
  name: "AccordeonDep",
  // components:{ StarGlyph },
  props: ["state"],
  data(){
    return {
      ui : {

        flexWrap: 'wrap',
  boxSizing: 'border-box',
  display: 'flex',
  position: 'sticky',
  width: 'calc(100% + 10px)',
  height: 'fit-content',
  backgroundColor: 'black',
  paddingLeft: '10px',
  paddingRight: '10px',
  marginTop: '10px',
  zIndex: '100',
  top:'10px'
      },
  ctnPlusMoins : {
  marginTop: 0,
  padding: 0 
    }
    }
  }
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

.button-closing {
  border-top: none;
  margin-right: 10px;
  margin-top: 0;
}
.button-parent {
  float: left;
  margin-right: 0;
}
button,
.button-parent {
  font-size: 16px;
  border: 1px solid white;
  color: white;
  background: none;
  font-family: "IBM Plex Mono", monospace;
  margin-bottom: 10px !important;
}
button {
  margin-right: 10px;
}
.button-plusMoins{
  margin-right: 0 !important;
  margin-left: 0 !important;
  margin-top: 0;
  width: 40px;
  border-left: none;
  height: 20px;
  display: block;
  line-height: 0;
}
.button-ctn-plusMoins {
  margin-top: 0 !important;
  padding: 0 !important;
}

.button-ctn-plusMoins,
button {
  margin-top: 10px !important;
  height: 40px !important;
}
</style>