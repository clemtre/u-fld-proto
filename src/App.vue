<template>
  <div id="app">
    <div
      class="header"
      v-bind:style="{
        display: classHeader.display,
        backgroundColor: classHeader.backgroundColor,
        height: classHeader.height,
      }"
    >

    <img :src="classHeader.src" alt="">
      <!-- <div class="gradient"></div> -->
    </div>
    <div class="header-padding"></div>
    <accordeon-dep :state="state" @stateBio="stateBio" @stateTel="stateTel">
    </accordeon-dep>
    <ul>
      <li v-for="projet in Projets" :key="projet.id">
        <div class="li-retrait">
        {{projet.titre | stripHTML}}

        </div>
        <!-- <hr class="li-hr"> -->
      </li>

    </ul>
    <!-- <p>
      {{ projet }}
    </p>-->
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex distinctio
      necessitatibus veniam, fugit expedita non blanditiis dignissimos iure qui
      rerum cupiditate quae omnis labore? Voluptates nam atque pariatur adipisci
      necessitatibus? Eius perferendis, quis quisquam magnam excepturi voluptate
      adipisci unde voluptatum sunt magni libero vitae eveniet alias doloribus
      iure sequi suscipit quaerat laudantium assumenda aspernatur pariatur
      dolorum itaque nulla? Iste, voluptates? Quisquam quaerat veniam fuga non!
      Iusto labore, deleniti consectetur sint rerum fuga. Nulla deserunt
      explicabo nostrum culpa. Harum earum consequatur officia eos rem id itaque
      vero totam. Sit, dolor alias. Unde eum modi quas impedit expedita incidunt
      itaque dolores ab aperiam. Necessitatibus recusandae nobis repellendus ut,
      ducimus ullam cumque sunt ipsum, sit delectus iste animi perspiciatis
      aliquam neque aliquid ipsam? Asperiores dicta, cumque quod molestias iusto
      illum temporibus facilis eaque unde non quia incidunt sunt sed est placeat
      perspiciatis voluptatibus omnis veniam debitis optio voluptates. Cum fuga
      at magnam culpa? Cum labore consequatur aliquid quae laboriosam assumenda
      suscipit sit, excepturi eum exercitationem iste dolore rerum, fugiat nisi
      eligendi modi quia numquam quod saepe earum, a debitis. Hic veniam id
      adipisci. Consequuntur ea, delectus magni ut voluptates, commodi minus et
      magnam tempore, amet deleniti? Nobis hic ipsam sed? Et quam hic unde,
      alias suscipit perferendis, eum odit mollitia sunt, natus dicta!
      Consectetur molestias, mollitia ipsam voluptatum velit est voluptatibus
      necessitatibus sint consequuntur repellendus libero pariatur quasi
      sapiente harum dolor ipsum, temporibus incidunt veniam earum. Libero
      delectus eum itaque sapiente sint debitis. Quia excepturi rem facilis
      rerum quaerat atque voluptatibus sapiente nihil labore sint qui suscipit
      perspiciatis quod esse possimus odit deserunt, unde perferendis numquam
      assumenda. Expedita unde minus cum vel nulla. Delectus illum ad laboriosam
      reiciendis explicabo officia accusantium, facere cumque! Labore, vel
      debitis veritatis pariatur culpa cupiditate, officiis aliquam, sint cum
      voluptatem similique! Autem sit, temporibus eos quam facilis molestias.
    </p>
  </div>
</template>

<script>
import Projets from "./assets/Projets.json";
import Images from "./assets/Images.json";
import AccordeonDep from "./components/AccordeonDep.vue";
import Vue from 'vue';

export default {
  name: "App",
  components: { AccordeonDep },

  data() {
    return {
      Projets: Projets.data,
      state: {
        bio: false,
        tel: false,
      },
      classHeader: {
        display: "none",
        backgroundColor: "yellow",
        height: "calc(100% - 20px)",
        src:require('./assets/output.png'),
        srcFlag:false
      },
    };
  },
  methods: {
    stateBio: function () {
      this.state.bio = !this.state.bio;
    },
    stateTel: function () {
      this.state.tel = !this.state.tel;
    },

    handleScroll() {
      // this.classHeader.backgroundColor = "#"+Math.round(Math.random()*10)+''+Math.round(Math.random()*10)+''+Math.round(Math.random()*10)
      console.log()
      const e = 100 - ((window.top.scrollY / window.innerHeight) * 100);
      this.classHeader.height = 'calc( '+ e + '% - 20px)';
      
      if (window.top.scrollY > window.innerHeight) {
        
        this.classHeader.display = "none";
      }
      else{
        this.classHeader.display = "block"
      }
    },
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll);
  },

  mounted() {
    console.clear();
    console.log(window.pageYOffset);
    if (window.pageYOffset === 0) {
      this.classHeader.display = "block";
    } else {

      this.classHeader.display = "none";
    }
    const images = Images.data;
    for (const projet of Projets.data) {
      if (projet.medias.length) {
        for (let media = 0; media < projet.medias.length; media++) {
          const imageRes = images.find((x) => x.id === projet.medias[media]);
          if (imageRes) {
            projet.medias[media] = imageRes.images.map(
              (x) => x.directus_files_id
            );
          }
        }
      }
    }
    // const projet = Projets.data.find((x) => x.slug === "farfetch");
    return {
      Projets,
    };
  },
};

Vue.filter('stripHTML', function (value) {
  const div = document.createElement('div')
  div.innerHTML = value
  const text = div.textContent || div.innerText || ''
  return text
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono&family=Libre+Baskerville:ital@0;1&display=swap');
* {
  font-size: 32px;
      color: black;
    font-family: 'Libre Baskerville', serif;
}

.li-hr {
  position: absolute;
}

html {
  overflow-x: hidden;
}
ul {
  padding:0
}
li:hover {
  font-style:oblique;
}
.li-retrait::before{
  background: url('./assets/uf-mono.png');
  background-size: 40px 40px;
    display: inline-block;
    width: 40px; 
    height: 40px;
    position: absolute;
    content:"";
    left: 10px;
    top: 5px;
}
.li-retrait {
  margin-left: 60px;
}
li{
  position: relative;
  line-height: 50px;
  border-bottom: 1px solid black;
  width: 100%;
  list-style-type: none;
}
button:active {
}

img {
  height: 100%;
  margin-left: 50%;
  transform: translateX(-50%);
  float: left;
  scale: 1;
  object-fit: contain;
  transform-origin: center;
}
 .header * {
  box-sizing: border-box;
}
.header {
  /* border: 10px solid black; */
  width: calc(100% - 20px);
  height: 100%;
  position: fixed;
  pointer-events: none;
}
body {
  width: calc(100% - 40px);
  margin : 10px
}
/* .header::after {
  width: 100%;
  height: 10px;
  background-color: green;
  position: absolute;
  top:0
} */
.header-padding {
  height: 100vh;
  height: calc(100vh - 10px);

  width: 100%;
}

</style>
