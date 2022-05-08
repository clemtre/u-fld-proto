<template>
  <div class="star-ctn">
      <span class="a" v-html="res"></span>
  </div>
</template>

<script>
export default {
    data(){
        return{
            res :''

        }
    },
    created(){
        for(let i = 0; i < 360 ; i += 45){

            this.res += `<p class="z" style="transform : rotate(`+i+`deg)">r</p> `
        }
    }
}
</script>

<style>
span {
    color: green;
}
.star-ctn {
    width: 60px;
    height: 60px;
    background-color: #f00;
    position: relative;
}
.z {
    top: 20px;
    left: 20px;
    height: 10px;
    /* width: fit-content; */
    position: absolute;
}
</style>