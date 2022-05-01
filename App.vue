<template>
  <div id="app">
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
     <nav class="navbar fixed-top navbar-light bg-light pt-0 pb-0">
        <div class="container-fluid" style="background-color: #aeade0;">          
          <a class="navbar-brand" href="/"> 
          <div class="img-max border-0" style="outline-color:#aeade0; background-color: #aeade0;">
            <img src="geekNest.svg" style="float:left;" class="pt-1 img-fluid"> 
          </div>
          </a>            
          </div>
      </nav>

      <modal name="about-modal" :adaptive="true">
        <div class="row grid px-3" style="font-size: 0.8em">
          <div class="col-md-6 text-start pt-4 px-4">
           
              <div class="img-max-about ml-3 mb-3">
                <img src="geekNestAbout.svg" class="img-fluid"> 
              </div>
              <p>
                Geek Nest is a tech news aggregator built in VueJS to keep up with tech news across platforms from one place. It is inspired by <a href="https://hackurls.com" target="_blank"> hackurls.com</a>, but with a different selection of sites.
              </p>

          </div>
          <div class="col-md-6 py-4 px-4 text-start">
            <strong>Milestones</strong> &#127882; 
            <br/><br/>
            1. Apr 29: Published the website <br/>
            2. Apr 30: Released the source<br/>
            3. May 1: Post on ShowHN <br/>
          </div>   
        </div>
        <div></div>
      </modal>

    <div class="px-5 pt-4"></div>
    <!-- HACKERNEWS -->
    <div class="px-5 pt-4">
      <h4>
        <a href="https://news.ycombinator.com" class="header-link" target="_blank">
          Hacker News
        </a>
      </h4>
    </div>
 
    <div class="text-start px-5 pb-0">
      <pulse-loader :loading="hnloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
    </div>


    <div class="row px-5">
      <!-- <div class="col-sm-0.5"/> -->
      <div class="col-sm-6 col-md-4">
        <ul class="review_bottom">
          <br>
          <li v-for="article in top_articles_data_hn.slice(0,10)" :key="article.id" class="pt-0 pb-0"> 
            <a :href="article.url" target="_blank">{{ article.title }}</a>
          </li>
          <br/>
        </ul>
      </div>
      <div class="col-sm-6 col-md-4">
        <ul class="review_bottom">
          <br>
          <li v-for="article in top_articles_data_hn.slice(10,20)" :key="article.id"> 
            <a :href="article.url" target="_blank">{{ article.title }}</a>
          </li>
          <br/>
        </ul>
      </div>
      <div class="col-sm-6 col-md-4">
        <ul class="review_bottom">
          <br>
          <li v-for="article in top_articles_data_hn.slice(20,30)" :key="article.id" class="pt-0 pb-0"> 
            <a :href="article.url" target="_blank">{{ article.title }}</a>
          </li>
          <br/>
        </ul>
      </div>
    </div>

    <div class="row px-5">
    <!-- PROGGIT -->
      <div class="col-sm-6 col-md-4">
        <div class="px-2 pt-1">
          <h4>
            <a href="https://old.reddit.com/r/programming/" class="header-link" target="_blank">
              r/Programming
            </a>
          </h4>
        </div>


        <div class="text-start px-5 pb-0 mb-4">
          <pulse-loader :loading="proggitloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
        </div>

        <ul class="review_bottom">
          <li v-for="article in top_articles_data_reddit.slice(0,10)" :key="article.permalink"> 
            <a :href="`https://www.reddit.com`+article.permalink" target="_blank">{{article.title }}</a>
          </li>
        </ul>
      </div>
<!-- TECHMEME -->
      <div class="col-sm-6 col-md-4">
        <div class="px-2 pt-1">
          <h4>
            <a href="https://techmeme.com" class="header-link" target="_blank">
              Techmeme
            </a>
          </h4>
        </div>

        <div class="text-start px-5 pb-0 mb-4">
          <pulse-loader :loading="techmemeloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
        </div>
        
        <ul class="review_bottom">
          <li v-for="article in top_articles_data_techmeme.slice(1,6)" :key="article[1].innerHTML"> 
            <a :href="article[1].innerHTML" target="_blank">{{article[0].innerHTML}}</a>
          </li>
        </ul>
      </div>
<!-- SLASHDOT -->
      <div class="col-sm-6 col-md-4">
        <div class="px-2 pt-1">
          <h4>
            <a href="https://slashdot.com" class="header-link" target="_blank">
              Slashdot
            </a>
          </h4>
        </div>

        <div class="text-start px-5 pb-0 mb-4">
          <pulse-loader :loading="slashdotloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
        </div>

        <ul class="review_bottom">
          <li v-for="article in top_articles_data_slashdot.slice(2,13)" :key="article[1].innerHTML"> 
            <a :href="article[1].innerHTML" target="_blank">{{article[0].innerHTML}}</a>
          </li>
        </ul>
      </div>
    </div>

      <div class="mt-5 mb-0">
        <p v-if="!showmoreflag" class="text-center" style="color: #7c7ae7" @click="showmore"><strong>See More</strong></p>
      </div>

      <div v-if="showmoreflag" class="m-0 p-0">
         <div class="row px-5">
        <!-- LOBSTERS -->
          <div class="col-sm-6 col-md-4">
            <div class="px-2 pt-1">
              <h4>
                <a href="https://lobste.rs" class="header-link" target="_blank">
                  Lobsters
                </a>
              </h4>
            </div>


            <div class="text-start px-5 pb-0 mb-4">
              <pulse-loader :loading="lobstersloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
            </div>

            <ul class="review_bottom">
              <li v-for="article in top_articles_data_lobsters.slice(1,15)" :key="article[1].innerHTML"> 
                <a :href="article[1].innerHTML" target="_blank">{{article[0].innerHTML}}</a>
              </li>
            </ul>
          </div>
    <!-- THE NEXT WEB -->
          <div class="col-sm-6 col-md-4">
            <div class="px-2 pt-1">
              <h4>
                <a href="https://thenextweb.com" class="header-link" target="_blank">
                  The Next Web
                </a>
              </h4>
            </div>

            <div class="text-start px-5 pb-0 mb-4">
              <pulse-loader :loading="nextwebloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
            </div>
            
            <ul class="review_bottom">
              <li v-for="article in top_articles_data_nextweb.slice(1,12)" :key="article[1].innerHTML"> 
                <a :href="article[1].innerHTML" target="_blank">{{article[0].innerHTML}}</a>
              </li>
            </ul>
          </div>
    <!-- PHORONIX -->
          <div class="col-sm-6 col-md-4">
            <div class="px-2 pt-1">
              <h4>
                <a href="https://www.phoronix.com/" class="header-link" target="_blank">
                  Phoronix
                </a>
              </h4>
            </div>

            <div class="text-start px-5 pb-0 mb-4">
              <pulse-loader :loading="phoronixloader" :color="loadercolor" :size="'8px'"></pulse-loader>    
            </div>

            
            <ul class="review_bottom">
              <li v-for="article in top_articles_data_phoronix.slice(1,11)" :key="article[1].innerHTML"> 
                <a :href="article[1].innerHTML" target="_blank">{{article[0].innerHTML}}</a>
              </li>
            </ul>
          </div>
         </div>
      </div>

      <div class="pb-3">
        <a href="mailto:geeknest.support@protonmail.com" class="contact"><span>Contact: geeknest.support@protonmail.com</span> </a> 
        &#8226;
        <a class="about" @click="showabout"> About</a>
      </div>
    </div>
</template>

<script>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
const API_URL_HN = "https://hacker-news.firebaseio.com/v0/topstories.json?print=pretty"
const API_URL_HN_ITEM = "https://hacker-news.firebaseio.com/v0/item/"

const API_URL_REDDIT = "https://api.pushshift.io/reddit/search/submission/?q=a&subreddit=programming&sort=score:desc&size=35&after=24h&fields=title,permalink"

const API_TECHMEME_URL = "http://www.techmeme.com/index.xml"

const API_SLASHDOT_URL = "http://rss.slashdot.org/Slashdot/slashdot"

const API_LOBSTERS_URL = "https://lobste.rs/rss"

const API_PHORONIX_URL = "https://www.phoronix.com/rss.php/"

const API_NEXTWEB_URL = "https://thenextweb.com/feed"

export default {
  name: 'app',
  data () {
    return {
      msg: 'Assortment of top news tech articles',
      top_hn_list: ['loading'],
      top_hn_data: ['uh??'],
      top_articles_data_hn : [],
      top_articles_data_reddit : [],
      top_articles_data_techmeme : [],
      top_articles_data_slashdot : [],
      top_articles_data_lobsters : [],
      top_articles_data_nextweb : [],
      top_articles_data_phoronix : [],

      hnloader: true,
      proggitloader: true,
      techmemeloader: true,
      slashdotloader: true,
      lobstersloader: true,
      nextwebloader: true,
      phoronixloader: true,

      label: 'Loading...',
      loadercolor: "#b46b52",
      loadersize: 50,
      news: true,

      showmoreflag: false,

      switch_options: {
        layout: {
          color: 'black',
          backgroundColor: 'lightgray',
          selectedColor: 'white',
          selectedBackgroundColor: 'green',
          borderColor: 'black',
          fontFamily: 'Arial',
          fontWeight: 'normal',
          fontWeightSelected: 'bold',
          squareCorners: true,
          noBorder: true
        },
        size: {
          fontSize: "0.5",
          height: "1",
          padding: "0",
          width: "6",
        },
        items: {
          delay: .4,
          preSelected: 'Tech',
          disabled: false,
          labels: [
            {name: 'Tech', color: 'black', backgroundColor: '#fbe29c'}, 
            {name: 'Career', color: 'black', backgroundColor: '#fbe29c'}
          ]
        }
      }

    }
  },
  created () {
  //   console.log("fetching articles data")
    this.fetchHNdata()
    this.fetchProggit()
    this.fetchTechmeme()
    this.fetchSlashdot()
  },
  components: {
    PulseLoader
  },
  methods: {
    async fetchHNdata() {
      const response = await fetch(API_URL_HN)
      const data = await response.json();
      this.top_hn_list_ids = data.slice(0,30)

      this.top_articles_data_hn = await Promise.all(this.top_hn_list_ids.map(async article_id => {
            const res = await fetch(`${API_URL_HN_ITEM}${article_id}.json`);
            return res.json();
      }));

      // truncate long titles
      this.top_articles_data_hn.forEach(element => {
        if (element.title.length > 120) {
          element.title = element.title.substring(0, 120) + "...";
        }
      });

      this.hnloader = false;

      this.top_hn_list_ids.forEach(element => this.top_hn_data.push({'id': element, 'url': `https://news.ycombinator.com/item?id=${element}`, 'title': "abcd"})
      ); 
    },
    async fetchProggit() {
      const response = await fetch(API_URL_REDDIT)
      const temp_top_articles_data_reddit = await response.json()


      this.top_articles_data_reddit =  temp_top_articles_data_reddit.data

      this.top_articles_data_reddit.forEach(element => {
        if (element.title.length > 120) {
          element.title = element.title.substring(0, 120) + "...";
        }
      });

      this.proggitloader = false;
    },

    async fetchTechmeme() {
      // get the data from "http://www.techmeme.com/index.xml"
      const response = await fetch(API_TECHMEME_URL).then(response => response.text())

      var parser = new DOMParser();
      const xml_data = parser.parseFromString(response, "application/xml")
      var temp_data = []
      const xml_data_titles = xml_data.getElementsByTagName("title");
      const xml_data_urls = xml_data.getElementsByTagName("link");

      var title_arr = Array.prototype.slice.call(xml_data_titles)
      var url_arr = Array.prototype.slice.call(xml_data_urls)

      var zip_data = title_arr.map(function(e, i) {
        return [e, url_arr[i]];
      });

      this.top_articles_data_techmeme = zip_data
      this.techmemeloader = false;
    },

    async fetchSlashdot() {
      // get the data from "http://rss.slashdot.org/Slashdot/slashdot"
      const response = await fetch(API_SLASHDOT_URL).then(response => response.text())

      var parser = new DOMParser();
      const xml_data = parser.parseFromString(response, "application/xml")
      var temp_data = []
      const xml_data_titles = xml_data.getElementsByTagName("title");
      const xml_data_urls = xml_data.getElementsByTagName("link");

      var title_arr = Array.prototype.slice.call(xml_data_titles)
      var url_arr = Array.prototype.slice.call(xml_data_urls)

      var zip_data = title_arr.map(function(e, i) {
        return [e, url_arr[i]];
      });

      this.top_articles_data_slashdot = zip_data
      this.slashdotloader = false;
    },
    async fetchLobsters() {
      // console.log("fetching data form lobsters")
      // get the data from "https://lobste.rs/rss"
      const response = await fetch(API_LOBSTERS_URL).then(response => response.text())

      var parser = new DOMParser();
      const xml_data = parser.parseFromString(response, "application/xml")
      var temp_data = []
      const xml_data_titles = xml_data.getElementsByTagName("title");
      const xml_data_urls = xml_data.getElementsByTagName("link");

      var title_arr = Array.prototype.slice.call(xml_data_titles)
      var url_arr = Array.prototype.slice.call(xml_data_urls)

      var zip_data = title_arr.map(function(e, i) {
        return [e, url_arr[i]];
      });

      this.top_articles_data_lobsters = zip_data
      this.lobstersloader = false;
    },
    async fetchNextWeb() {
      // console.log("fetching data form next web")
      const response = await fetch(API_NEXTWEB_URL).then(response => response.text())

      var parser = new DOMParser();
      const xml_data = parser.parseFromString(response, "application/xml")
      var temp_data = []
      const xml_data_titles = xml_data.getElementsByTagName("title");
      const xml_data_urls = xml_data.getElementsByTagName("link");

      var title_arr = Array.prototype.slice.call(xml_data_titles)
      var url_arr = Array.prototype.slice.call(xml_data_urls)

      var zip_data = title_arr.map(function(e, i) {
        return [e, url_arr[i]];
      });

      this.top_articles_data_nextweb = zip_data
      this.nextwebloader = false;
    },
    async fetchPhoronix() {
      // console.log("fetching data form phoronix")
      const response = await fetch(API_PHORONIX_URL).then(response => response.text())

      var parser = new DOMParser();
      const xml_data = parser.parseFromString(response, "application/xml")
      var temp_data = []
      const xml_data_titles = xml_data.getElementsByTagName("title");
      const xml_data_urls = xml_data.getElementsByTagName("link");

      var title_arr = Array.prototype.slice.call(xml_data_titles)
      var url_arr = Array.prototype.slice.call(xml_data_urls)

      var zip_data = title_arr.map(function(e, i) {
        return [e, url_arr[i]];
      });

      this.top_articles_data_phoronix = zip_data
      this.phoronixloader = false;
    },
    showmore() {
      this.showmoreflag = true;
      this.fetchLobsters();
      this.fetchNextWeb();
      this.fetchPhoronix();
    },
    showabout() {
      this.$modal.show('about-modal');
    }
  },
}

</script>

<style>
img {
  max-width: 15%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
  font-size: 0.75em;
}

.modal {
  font-size: 0.65em;
}

h1, h2, h3, h4 {
  font-weight: normal;
  text-align: left;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  text-align: left;
  display: block;
  margin: 0 10px;
  margin-bottom: 0.9em;
  line-height: 1.1em;
}

a {
  /* color: #42b983; */
  /* color: #b46b52; */
  color: #7a5510;
  text-decoration: none;
}

#page-title {
  color: #b8ae72;
}

a.header-link {
  color: #7c7ae7;
  text-decoration: none;
}

a.contact,a.about {
  font-size: 0.9em;
  color: #2c3e50;
  text-decoration: none;
  cursor: pointer;
}

.img-max {
  max-width: 200px;
}

.img-max-about {
  max-width: 100px;
  margin: -2px 0 0 -2px;
}

.bullets li {
 list-style-type: circle;
}

</style>
