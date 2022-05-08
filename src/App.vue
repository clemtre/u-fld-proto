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
      <img width="2000" :src="classHeader.src" alt="" />
      <!-- <div class="gradient"></div> -->
    </div>
    <div class="header-padding"></div>
    <accordeon-dep
      :state="state"
      @changeimg="changeimg"
      @statebio="statebio"
      @stateTel="stateTel"
    >
    </accordeon-dep>
    <section class="bio" v-if="state.bio">
      <p v-html="Bio.descriptif"></p>
      <hr />
    </section>
    <ul>
      <li class="projet" v-for="projet in Projets" :key="projet.id">
        <img
          class="entete"
          v-bind:style="{ maxHeight: classImg.heightRet }"
          :src="
            'https://porte-secrete.unexploredfields.com/assets/' +
            projet.entete +
            '?quality=20'
          "
          alt=""
        />
        <div class="li-retrait" v-if="projet.entete">
          <h2>
            {{ projet.titre | stripHTML }}
            </h2>
          <br />
          <h2>
            {{ projet.nomClient | stripHTML }}
          </h2>
          <section class="meta">

          <h3>{{ projet.date }}</h3>
          <h3 v-if="projet.formats_et_techniques">{{ projet.formats_et_techniques }}</h3>
          <h3 v-if="projet.credits">{{ projet.credits }}</h3>
          </section>
        </div>
        <!-- <hr class="li-hr"> -->
      </li>
    </ul>
    <!-- <p>
      {{ projet }}
    </p>-->
  </div>
</template>

<script>
import Projets from "./assets/Projets.json";
import Images from "./assets/Images.json";
import Clients from "./assets/Clients.json";
import Bio from "./assets/Bio.json";
import AccordeonDep from "./components/AccordeonDep.vue";

import "./assets/global.css";

import Vue from "vue";

export default {
  name: "App",
  components: { AccordeonDep },

  data() {
    return {
      Bio: Bio.data,
      Projets: Projets.data,
      state: {
        bio: false,
        tel: false,
      },
      classHeader: {
        display: "none",
        backgroundColor: "yellow",
        height: "calc(100% - 20px)",
        src: require("./assets/output.png"),
        srcFlag: false,
      },
      classImg: {
        height: 90,
        heightRet: "90vh",
      },
    };
  },
  methods: {
    changeimg(event) {
      console.log(event);
      this.classImg.height -= event;
      this.classImg.heightRet = this.classImg.height + "vh";
    },
    statebio: function () {
      this.state.bio = !this.state.bio;
    },
    stateTel: function () {
      this.state.tel = !this.state.tel;
    },

    handleScroll() {
      // this.classHeader.backgroundColor = "#"+Math.round(Math.random()*10)+''+Math.round(Math.random()*10)+''+Math.round(Math.random()*10)
      console.log();
      const e = 100 - (window.top.scrollY / window.innerHeight) * 100;
      this.classHeader.height = "calc( " + e + "% - 20px)";

      if (window.top.scrollY > window.innerHeight) {
        this.classHeader.display = "none";
      } else {
        this.classHeader.display = "block";
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
    console.log(window.pageYOffset);
    if (window.pageYOffset === 0) {
      this.classHeader.display = "block";
    } else {
      this.classHeader.display = "none";
    }
    const images = Images.data;
    for (const projet of Projets.data) {
      const nomClient = Clients.data.find((x) => x.id === projet.client);
      projet.nomClient = nomClient.nom;
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
    Projets.data.sort((a, b) => (a.ordre > b.ordre ? 1 : -1));
    // const projet = Projets.data.find((x) => x.slug === "farfetch");
    return {
      Projets,
    };
  },
};

//plutot le faire dans le cms
Vue.filter("cesureNoms", function (value) {
  const res = value.replace(/\b[A-Z][a-z0-9]+\s\b[A-Z][a-z0-9]+/g, "aa");
  console.log(value);
  return res;
});

Vue.filter("stripHTML", function (value) {
  const div = document.createElement("div");
  div.innerHTML = value;
  const text = div.textContent || div.innerText || "";
  return text;
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Mono&family=Libre+Baskerville:ital@0;1&display=swap");
* {
  font-size: 32px;
  color: black;
  font-family: "Libre Baskerville", serif;
}
.projet:hover {
  background-color: yellow;
}
.entete {
  max-height: 90vh;
}

.li-hr {
  position: absolute;
}
.bio {
  position: sticky;
}
html {
  /* overflow-x: hidden; */
}
ul {
  padding: 0;
}
li:hover {
  font-style: oblique;
}
.li-retrait::before {
  background: url("./assets/uf-mono.png");
  background-size: 40px 40px;
  display: inline-block;
  width: 40px;
  height: 40px;
  position: absolute;
  content: "";
  left: 10px;
  bottom: 50px;
}
.li-retrait {
  margin-left: 60px;
}
li {
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
  width: 100%;
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
  margin: 10px;
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
