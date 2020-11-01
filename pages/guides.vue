<template>
  <div id="id">
    <v-app>
      <div class="content" v-if="!loading">
        <div class="blogs">
          <section class="blogs-section section2">
            <div class="contents">
              <h3 class="subtit">Guides</h3>
              <ul class="list_news">
                <li v-for="blog in blogs" :key="blog.id" class="">
                  <div>
                    <img
                      :src="blog.image"
                      :alt="blog.title"
                      class="news_bnn"/>
                    <div class="news_tit" >
                      <router-link :to="{name: 'guide-slug', params: {slug: blog.slug}}">
                        <strong class="type">{{ blog.category }}</strong>
                        <span class="tit" v-ripple>{{ blog.title }}</span>
                      </router-link>
                    </div>
                  </div>
                </li>
              </ul>
            </div>
          </section>
        </div>
      </div>
      <infinite-loading v-if="!loading" spinner="waveDots" @infinite="loadmore">
          <div slot="no-more">End</div>          
      </infinite-loading>
    </v-app>
  </div>
</template>
<script>
import axios from "axios";
import { constant } from '@/plugins/Constant';
import InfiniteLoading from "vue-infinite-loading";

export default {
  name: "Blogs",
  components: {
    InfiniteLoading
  },
  head() {
    let title_ = "Guides, Tips and Events for Ragnarok Mobile Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/guides'
    let keywords_ = title_ + ', ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Your ultimate guide for Ragnarok Mobile Eternal Love. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
    return {
      title: title_,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: description_
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: keywords_
        },
        {
          hid: 'og:title',
          name: 'og:title',
          content: title_
        },
        {
          hid: 'og:description',
          name: 'og:description',
          content: description_
        },
        {
          hid: 'og:url',
          name: 'og:url',
          content: url_
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: 'https://www.ragnarokmobile.net/img/louyang.webp'
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: description_
        },
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: title_
        },
      ],
      link: [
        {
          rel: 'canonical',
          href: url_
        }
      ]
    }
  },
  data() {
    return {
      fullPage: true,
      url: constant.url,
      loading: true,
      blogs: [],
      page: 2
    };
  },
  methods: {
    getBlogs() {
      axios
        .get(constant.getBlogs)
        .then(response => (
          this.blogs = response.data.data
        ))
        .catch(error => {})
        .finally(() => {this.loading = false})
    },
    loadmore($state) {
      let vm = this;
      axios
        .get(constant.getBlogs + "?page=" + vm.page)
        .then(response => {
          response.data.data.map(function(value) {
            vm.blogs.push(value);
          });
          vm.page += 1;
          $state.loaded();
        })
        .catch(error => console.log(error))
        .finally(() => console.log());
    },
  },
  mounted() {
    this.getBlogs();
  }
};
</script>
<style lang="scss">
@import '../assets/scss/mixins.scss';
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
  }
}
.blogs-section {
  .contents {
    margin: 0 auto;
  }
  ul {
    padding-left: 0 !important;
    &.list_news {
      flex-wrap: wrap;
      display: flex;
      margin: 14px auto 0;
      justify-content: center;
      place-content: space-between;
      .news_bnn {
        width: 290px;
        object-fit: cover;
        height: 150px;
        box-shadow: 5px 5px 8px rgba(0, 0, 0, 0.3);

        @media only screen and (max-width: 768px) {
          width: 100%;
        }
      }
      li {
        width: 290px;
        margin-bottom: 20px;
        
        @media only screen and (max-width: 768px) {
          width: 100%;
        }
      }
      .news_tit {
        display: table;
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
          overflow: hidden;
          text-overflow: ellipsis;
          display: -webkit-box;
          -webkit-line-clamp: 2;
          -webkit-box-orient: vertical;
          height: 30px;
          color: #0c0c0c;
          font-size: 13px;
          line-height: 15px;
        }
      }
    }
  }
}
</style>