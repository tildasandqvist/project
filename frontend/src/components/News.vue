<template>
  <div class="container">
    <div class="row">
      <div class="artbig">
        <div class="col m-3">
          <img :src="articles[0].urlToImage" class="artbildbig" />
          <h2 class="arttitlebig">{{articles[0].title}}</h2>
          <p class="arttextbig">{{articles[0].content}}</p>
        </div>
      </div>
      <div class="w-100"></div>
      <div class="container-fluid" v-if="articles !== null">
        <div class="row">
          <div class="col-md-6" v-for="arts in articles.slice(1, 2)" :key="arts.title">
            <!------------------------------ COLUMN LEFT 1 ------------------------------>
            <div class="col1">
              <img :src="arts.urlToImage" class="col-bild-sec" />
              <h2 class="col-title-sec">{{arts.title}}</h2>
              <p class="col-text-sec">{{arts.content}}</p>
            </div>
          </div>

          <div class="col-md-6" id="overflow">
            <h4 class="livescore-title">LIVE TABLE</h4>
            <div class="nextprevbuttons">
              <button class="BUTTON_VMF" @click="component = 'firsttable' ">
                <p>La Liga</p>
              </button>
              <button class="BUTTON_VMF" @click="component = 'secondtable'">
                <p>Premier League</p>
              </button>
              <button class="BUTTON_VMF" @click="component = 'thirdtable'">
                <p>Serie A</p>
              </button>
            </div>

            <!-- This is where the components of the tables are being imported and shown onto this page -->
            <component :is="component"></component>
            <!-- Tables end here -->
          </div>
        </div>
      </div>

      <div class="w-100"></div>
      <div class="col m-3" id="deleted-media-col">
        <img :src="articles[3].urlToImage" class="artbild" />
        <h2 class="arttitle">{{articles[3].title}}</h2>
        <p class="arttext">{{articles[3].content}}</p>
      </div>
      <div class="col m-3">
        <img :src="articles[4].urlToImage" class="artbild" />
        <h2 class="arttitle">{{articles[4].title}}</h2>
        <p class="arttext">{{articles[4].content}}</p>
      </div>
      <div class="w-100"></div>
      <div class="col m-3" id="deleted-media-col2">
        <img :src="articles[6].urlToImage" class="artbild" />
        <h2 class="arttitle">{{articles[6].title}}</h2>
        <p class="arttext">{{articles[6].content}}</p>
      </div>
      <div class="col m-3">
        <img :src="articles[7].urlToImage" class="artbild" />
        <h2 class="arttitle">{{articles[7].title}}</h2>
        <p class="arttext">{{articles[7].content}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import firsttable from "./firsttable.vue";
import secondtable from "./secondtable.vue";
import thirdtable from "./thirdtable.vue";

export default {
  name: "News",
  components: {
    firsttable,
    secondtable,
    thirdtable
  },
  created() {
    fetch("/data.json")
      .then(response => response.json())
      .then(result => {
        this.articles = result[2].articles;
        console.log(result[2].articles[0].id);
      });
    fetch("http://localhost:3000/")
      .then(response => response.json())
      .then(result => {
        console.log(result);
        this.livescore = result.livescore;
        console.log(result.livescore[0]);
      });
  },
  data() {
    return {
      articles: null,
      livescore: null,
      component: "firsttable"
    };
  }
};
</script>

<style scoped>
.nextprevbuttons {
  text-align: center;
  margin-bottom: 7px;
}
.BUTTON_VMF {
  background: #ff9900;
  background-image: -webkit-linear-gradient(top, #ff9900, #ff9900);
  background-image: -moz-linear-gradient(top, #ff9900, #ff9900);
  background-image: -ms-linear-gradient(top, #ff9900, #ff9900);
  background-image: -o-linear-gradient(top, #ff9900, #ff9900);
  background-image: linear-gradient(to bottom, #ff9900, #ff9900);
  -webkit-border-radius: 8px;
  -moz-border-radius: 8px;
  border-radius: 8px;
  color: #ffffff;
  font-size: 15px;
  font-weight: 200;
  padding: 7px;
  text-decoration: none;
  display: inline-block;
  cursor: pointer;
  text-align: center;
  margin-right: 5px;
  height: 2.5em;
  text-decoration-style: solid;
  font-family: "Fira Sans", sans-serif;
}

.BUTTON_VMF:hover {
  border: solid rgba(255, 255, 255, 0) 1px;
  background: #455a64;
  background-image: -webkit-linear-gradient(top, #455a64, #455a64);
  background-image: -moz-linear-gradient(top, #455a64, #455a64);
  background-image: -ms-linear-gradient(top, #455a64, #455a64);
  background-image: -o-linear-gradient(top, #455a64, #455a64);
  background-image: linear-gradient(to bottom, #455a64, #455a64);

  text-decoration: none;
  height: 2.5em;
}
#overflow {
  overflow: auto;
  max-height: 26.7em;
}
/* Kolumner och deras innehåll:  */
.container-fluid {
  margin-bottom: -3em;
}
.col1 {
  background-color: rgb(255, 255, 255);
  height: 26.6em;
  float: right;
  box-shadow: 0 0 10px 5px rgba(129, 129, 129, 0.089);
  margin-bottom: 1em;
}
.col-bild-sec {
  margin-top: 25px;
  margin-bottom: 20px;
  float: left;
  width: 350px;
  height: 220px;
  margin-right: 15px;
  box-shadow: 1px 2px 10px 5px rgba(82, 82, 82, 0.068);
  border-radius: 2px;
  margin: 1em;
}

.col-text-sec {
  margin-top: 15px;
  margin-bottom: 15px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 14px;
  padding: 1em;
}
.col-title-sec {
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 20px;
  padding: 1em;
}
.col-author-sec {
  float: right;
  font-size: 15px;
  font-family: "Fira Sans", sans-serif;
  text-align: justify; /* For Edge */
  text-align-last: right;
  margin-right: 10px;
}

.row {
  margin-top: -6em;
  margin-bottom: 3em;
}
.col {
  background-color: rgb(255, 255, 255);
  height: auto; /* GÖR DENNA TILL AUTO SEN */
  float: right;
  box-shadow: 0 0 10px 5px rgba(129, 129, 129, 0.089);
}
.col-bild {
  margin-top: 25px;
  margin-bottom: 20px;
  float: left;
  width: 240px;
  height: 170px;
  margin-right: 15px;
  box-shadow: 1px 2px 10px 5px rgba(82, 82, 82, 0.068);
  border-radius: 2px;
}

.col-text {
  margin-top: 15px;
  margin-bottom: 15px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 14px;
}
.col-title {
  margin-top: 20px;
  margin-bottom: 10px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 20px;
}
.col-author {
  float: right;
  margin-top: 10px;
  font-size: 15px;
  font-family: "Fira Sans", sans-serif;
  text-align: justify; /* For Edge */
  text-align-last: right;
}
.col-bild2 {
  margin-top: 25px;
  margin-bottom: 20px;
  float: left;
  width: 240px;
  height: 170px;
  margin-right: 15px;
  box-shadow: 1px 2px 10px 5px rgba(82, 82, 82, 0.068);
  border-radius: 2px;
}

.col-text2 {
  margin-top: 15px;
  margin-bottom: 15px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 14px;
}
.col-title2 {
  margin-top: 20px;
  margin-bottom: 10px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 20px;
}
.livescore-title {
  text-align: center;
  margin-bottom: 3px;
  font-family: "Fira Sans", sans-serif;
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
}
.tr {
  text-align: center;
}
.td {
  text-align: center;
}
.artbild {
  margin-top: 25px;
  margin-bottom: 20px;
  float: left;
  width: 240px;
  height: 170px;
  margin-right: 15px;
  box-shadow: 1px 2px 10px 5px rgba(82, 82, 82, 0.068);
  border-radius: 2px;
}
.arttext {
  margin-top: 15px;
  margin-bottom: 15px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 14px;
}

.arttitle {
  margin-top: 20px;
  margin-bottom: 10px;
  font-family: "Fira Sans", sans-serif;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
  font-size: 20px;
}

/* TOP NYHETEN */
.artbig {
  margin-bottom: 6em;
  margin-left: 2em;
}
.artbildbig {
  margin-top: 20px;
  margin-bottom: 20px;
  float: left;
  width: 350px;
  height: 230px;
  margin-right: 15px;
  box-shadow: 1px 2px 10px 5px rgba(82, 82, 82, 0.068);
  border-radius: 2px;
}
.arttextbig {
  margin-bottom: 15px;
  font-family: "Fira Sans", sans-serif;
  font-size: 16px;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
}
.arttitlebig {
  margin-top: 15px;
  margin-bottom: 7px;
  font-family: "Fira Sans", sans-serif;
  font-size: 26px;
  color: rgba(0, 0, 0, 0.842);
  text-shadow: 2px 2px 3px rgba(82, 82, 82, 0.068);
}
@media (max-width: 376px) {
  .artbildbig {
    width: 100%;
    height: 50%;
    margin-bottom: 10px;
  }
  .arttitlebig {
    font-size: 20px;
  }
  .arttextbig {
    font-size: 15px;
  }
  .col-bild-sec {
    float: none;
    width: 100%;
    height: 50%;
    margin: 0;
  }
  .col-title-sec {
    padding: 0em;
    margin-top: 10px;
  }
  .col1 {
    height: auto;
    padding: 1em;
  }
  .col-text-sec {
    padding: 0;
  }
  #deleted-media-col {
    display: none;
  }
  #deleted-media-col2 {
    display: none;
  }
  .artbild {
    width: 100%;
    height: 50%;
  }
}
</style>