<template>
  <div id="app">
    <v-app>
      <div class="home-content">
        <section class="hero section1 mt-12">
          <div class="message-container">
            <div class="site-title">
              <h4>
                Ragnarok Mobile
                <sup>v2</sup>
              </h4>
            </div>
            <div class="site-message">
              Here you will find
              <strong>Guides</strong>,
              <strong>Tips</strong>, and game database such as Monsters, Cards, Items and more that will help you in the game.
            </div>
          </div>
        </section>
        <section class="section3 mt-5">
          <h3 class="subtit mb-3">Ragnarok Mobile Database</h3>
          <div class="row no-gutters">
            <router-link  tabindex :to="{ name: 'monsters'}" class="col col-3">
              <div>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/monster-icon.png" alt="Ragnarok Mobile Monster Icon"/>
                  <span>Monster</span>
                </div>
              </div>
            </router-link>
            <router-link tabindex :to="{ name: 'cards'}" class="col col-3">
              <div>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/card-icon.png" alt="Ragnarok Mobile Card Icon"/>
                  <span>Card</span>
                </div>
              </div>
            </router-link>
            <router-link tabindex :to="{ name: 'equipments'}" class="col col-3">
              <div>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/armor-icon.png" alt="Ragnarok Mobile Equipment Icon"/>
                  <span>Equipment</span>
                </div>
              </div>
            </router-link>
            <router-link tabindex :to="{ name: 'headwears'}" class="col col-3">
              <div>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/headwear-icon.png" alt="Ragnarok Mobile Headwear Icon"/>
                  <span>Headwear</span>
                </div>
              </div>
            </router-link>
              <router-link tabindex :to="{ name: 'furnitures'}" class="col col-3">
              <div>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/furniture-icon.png" alt="Ragnarok Mobile Furniture Icon"/>
                  <span>Furniture</span>
                </div>
              </div>
              </router-link>
              <router-link tabindex :to="{ name: 'pets'}" class="col col-3">
              <div>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/pet-icon.png" alt="Ragnarok Mobile Pet Icon"/>
                  <span>Pet</span>
                </div>
              </div>
            </router-link>
              <div class="col col-3" tabindex>
                <div class="icons">
                  <img class="icon" src="../assets/images/icons/food-icon.png" alt="Ragnarok Mobile Food Icon"/>
                  <span>Food</span>
                </div>
              </div>
          </div>
        </section>

        <section class="appicons mt-2 mb-5">
          <div class="apps container center mt-4">
            <router-link tabindex :to="{name: 'endless-tower'}" class="playstore col-12" v-ripple>
              Endless Tower MVP/Mini List (SEA)
            </router-link>
            <router-link tabindex :to="{name: 'valhalla-ruins'}" class="appstore col-12" v-ripple>
              Valhalla Ruins Map
            </router-link>  
            <!-- <div class="playstore mr-3">
              <img src="../assets/images/google-play-badge/128x128.png" alt="Download to playstore">
            </div>
            <div class="appstore ml-3">
              <img src="../assets/images/app-store-badge/128x128.png" alt="Download to appstore">
            </div> -->
          </div>

        </section>
        <section class="main_news section2">
          <div class="contents">
            <h3 class="subtit">Guides</h3>
            <ul class="list_news">
              <li>
                  <div class="news_tit" v-ripple>
                    <router-link tabindex :to="{name: 'guides-safe-refining-guide'}" class="d-flex pointer">
                      <span @click="$router.push({name: 'guides-safe-refining-guide'})" class="tit">Safe Refining Guide</span>
                    </router-link>
                  </div>
              </li>
              <li>
                  <div class="news_tit" v-ripple>
                    <router-link tabindex :to="{name: 'guides-quiz'}" class="d-flex pointer">
                      <span @click="$router.push({name: 'guides-quiz'})" class="tit">Monster quiz in Wasteland</span>
                    </router-link>
                  </div>
              </li>
              <li v-for="blog in BlogsToDisplay" :key="blog.id" class>
                  <div class="news_tit" v-ripple>
                    <router-link tabindex :to="{name: 'guide', params: {slug: blog.slug}}" class="d-flex pointer">
                      <span @click="$router.push({name: 'guide', params: {slug: blog.slug}})" class="tit">{{ blog.title }}</span>
                    </router-link>
                  </div>
              </li>
            </ul>
            <v-col class="text-center" cols="12" sm="12">
              <router-link tabindex :to="{name: 'guides'}">
                <div class="my-2 see-more" v-ripple @click="$router.push({name: 'guides'})" tabindex>
                  <span>Click here to see more guides</span>
                </div>
              </router-link>
            </v-col>
          </div>
        </section>
        <section class="footer-section">
          <p class="copyright center">
            © RagnarokMobile.net 2018 - 2020 | All Rights Reserved</p>
          <p class="mt-n3">
            We are
            <strong>NOT</strong> affiliated with
            <strong>Ragnarok M: Eternal Love</strong>, this is a
            <strong>fan site</strong> dedicated to the game. Game related images and contents are copyrighted by Gravity Co. and X.D. Global Ltd.
          </p>
          <div class="socia-icons center mt-n3">
            <a href="https://www.facebook.com/ragnarokmobile.net/" target="_blank" rel="noopener" aria-label="Follow and Like us on Facebook">
            <v-btn
              aria-label="Follow and Like us on Facebook"
              color="white"
              class="white--text"
              fab
              icon
              small>
              <v-icon>mdi-facebook</v-icon>
            </v-btn>
            </a>
            <a href="https://www.youtube.com/channel/UCMjfudA3s5DTcdVTbdBqCWQ" target="_blank" rel="noopener" aria-label="Subscribe to our Youtube channel">
            <v-btn
              aria-label="Subscribe to our Youtube channel"
              color="white"
              class="white--text"
              fab
              icon
              small>
              <v-icon>mdi-youtube</v-icon>
            </v-btn>
            </a>
          </div>
          <small class="legal center">
            <router-link :to="{ name: 'privacy'}">
              <div v-ripple @click="$router.push({name: 'privacy'})" class="pointer">Privacy Policy</div> 
            </router-link>|
            <router-link :to="{ name: 'contact'}">
              <div v-ripple @click="$router.push({name: 'contact'})" class="pointer">Contact Us</div>
            </router-link>
          </small>
        </section>
      </div>
    </v-app>
  </div>
</template>

<script>
import axios from "axios";
import { constant } from "@/plugins/Constant";
export default {
  layout: 'default',
  head() {
    return {
      title: 'Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Your ultimate guide for Ragnarok Mobile Eternal Love. ROM SEA, ROM Global, ROM Europe. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
        }
      ],
    }
  },
  data() {
    return {
      colors: [
        "indigo",
        "warning",
        "pink darken-2",
        "red lighten-1",
        "deep-purple accent-4"
      ],
      blogs: [],
      socials: [
        {
          icon: 'mdi-facebook',
          color: 'white',
        },
        {
          icon: 'mdi-youtube',
          color: 'white',
        },
      ],
    };
  },
  mounted() {
    this.getBlogs();
  },
  computed: {
    BlogsToDisplay: function() {
      return this.blogs.slice(0, 10);
    }
  },
  methods: {
    getBlogs() {
      axios
        .get(constant.getBlogs)
        .then(response => (this.blogs = response.data.data))
        .catch(error => {})
        .finally(() => {});
    }
  }
};
</script>
<style lang="scss">
.home-content {
  background: #fff;
}
.v-carousel {
  height: 200px !important;
}
.catagory-card {
  position: relative;
  z-index: 1;
  text-align: center;
  border-radius: 0.75rem;
  border-color: transparent !important;
  border-radius: 1rem;
  box-shadow: 0 1px 1px 0px #d7def4;
  .card-body {
    padding: 1rem;
    flex: 1 1 auto;
    min-height: 1px;
    padding: 1.25rem;
  }
  a {
    display: block;
    padding-top: 0.25rem;
    padding-bottom: 0.25rem;
    transition-duration: 500ms;
    text-decoration: none;
    outline: 0 solid transparent;
    box-shadow: none;
  }
  i {
    margin-bottom: 0.75rem;
    font-size: 1.75rem;
    display: block;
    color: #100dd1;
  }
  span {
    transition-duration: 500ms;
    display: block;
    font-size: 12px;
    font-weight: 700;
    line-height: 1;
    color: #747794;
  }
}
.card {
  position: relative;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-direction: column;
  flex-direction: column;
  min-width: 0;
  word-wrap: break-word;
  background-color: #fff;
  background-clip: border-box;
  border: 1px solid rgba(0, 0, 0, 0.125);
  border-radius: 0.25rem;
}
.section1 {
  background: url("../assets/images/louyang.webp");
  background-size: cover;
  .message-container {
    background: rgba(0, 0, 0, 0.7);
    padding: 90px 50px;
    color: #fff;
    @media only screen and (max-width: 768px) {
      padding: 50px;
    }
    .site-title {
      text-align: center;
      font-size: 18px;
      text-transform: uppercase;
      font-weight: bold;
    }
    .site-message {
      margin-top: 10px;
      text-align: center;
      font-size: 15px;
    }
  }
}
.section2 {
  padding: 0 10px;
  margin-top: 15px;
  .more-news {
    color: $white;
    background-color: $primary !important;
    padding: 0 40px !important;
  }
  .see-more {
    cursor: pointer;
    font-size: 0.9em;
    text-transform: uppercase;
    font-weight: 500;
    color: $primary;
  }
}
.section3 {
  .icons {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px !important;
    transition: opacity 0.2s cubic-bezier(0.4, 0, 0.6, 1);
    cursor: pointer;
    .icon {
      width: 40px;
    }
    span {
      color: $primary;
      line-height: 23px;
      font-size: 0.9rem;
      font-weight: 400;
    }
    &:hover {
      background: #eee;
      border-radius: 5px;
    }
    &:focus {
      background: #eee;
      border-radius: 5px;
    }
  }
}
.section4 {
  ._30ChT {
    height: 74px;
    display: flex;
    position: relative;
    margin: 0 5px;
  }
  ._3sZO4 {
    box-shadow: hsl(0, 0%, 80%) 0 5px 16px;
    padding: 0 50px 0 32px;
    width: 100%;
    flex: 1 auto;
    box-sizing: border-box;
    border: 0;
    border-radius: 5;
    color: gray;
    font-size: 16px;
    line-height: normal;
    height: 100%;
    padding: 10px 50px 10px 20px;
    @media only screen and (max-width: 768px) {
      padding: 20px;
    }
    &:focus {
      width: 100%;
      transition: 0.5s;
      box-shadow: hsl(0, 0%, 80%) 0 5px 16px;
    }
  }
  .input-icon {
    color: $primary;
    width: 46px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    right: 8px;
    top: 13px;
  }
}
.footer-section {
  background-color: $primary;
  padding: 50px 20px 20px;
  p {
    color: $white;
    font-size: 13px;
    text-align: center;
    line-height: 23px;
    text-overflow: ellipsis;
  }
  .legal {
    color: $white;
    display: flex;
    place-content: center;
    text-overflow: ellipsis;
    div {
      margin: 0px 10px;
    }
    a {
      color: $white !important;
    }
  }
}
.main_news {
  .contents {
    margin: 0 auto;
  }
  ul {
    padding-left: 0 !important;
    &.list_news {
      flex-wrap: wrap;
      display: flex;
      flex-direction: column;
      margin: 14px auto 0;
      @media only screen and (max-width: 768px) {
        place-content: space-between;
      }
      .news_bnn {
        width: 280px;
        object-fit: cover;
        height: 150px;
        box-shadow: 5px 5px 8px rgba(0, 0, 0, 0.3);

        @media only screen and (max-width: 768px) {
          width: 100%;
          height: 200px;
        }
      }
      li {
        margin-left: 10px;

        @media only screen and (max-width: 768px) {
          margin-left: 0px;
          width: 100%;
          margin-bottom: 12px;
        }
      }
      .news_tit {
        display: flex;
        padding: 8px 4px 0;
        .type {
          display: table-cell;
          width: 1%;
          padding-right: 4px;
          font-size: 12px;
          font-weight: 400;
          letter-spacing: 0.05em;
          color: $primary;
          &:before {
            content: "#";
          }
        }
        .tit {
          height: 30px;
          color: #0c0c0c;
          font-size: 15px;
          line-height: 15px;
          @media only screen and (max-width: 768px) {
            line-height: 20px;
          }
        }
      }
    }
  }
}
.copyright {
  color: $white;
  display: flex;
  place-content: center;
}
</style>