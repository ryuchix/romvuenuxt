<template>
  <div id="app">
    <v-app>
      <div class="content blog" v-if="!loading">
        <div class="board_head">
          <strong class="type">{{ blog.category }}</strong>
          <time datetime="2019-01-02">2020-06-08</time>
          <h3 class="tit">{{ blog.title }}</h3>
        </div>
        <div class="board_body">
          <img :alt="blog.title" :src="blog.image" style="margin-bottom: 15px" />
          <div>
            <div
              class="fb-like"
              style="margin-bottom: 5px;"
              :data-href="'https://www.ragnarokmobile.net/guide/'+blog.slug"
              data-layout="standard"
              data-action="like"
              data-size="small"
              data-show-faces="true"
              data-share="true">
            </div>
          </div>
          <div class="body" v-html="blog.content"></div>
        </div>
        <div class="comments">
          <div
            class="fb-like"
            style="margin-bottom: 5px;"
            :data-href="'https://www.ragnarokmobile.net/guide/'+blog.slug"
            data-layout="standard"
            data-action="like"
            data-size="small"
            data-show-faces="true"
            data-share="true"></div>
          <div class="pad30"></div>
          <div
            class="fb-comments"
            :data-href="'https://www.ragnarokmobile.net/guide/'+blog.slug"
            data-numposts="5"
            data-width="100%"></div>
        </div>
      </div>
    </v-app>
  </div>
</template>
<script>
import axios from "axios";
import { constant } from '@/plugins/Constant';

export default {
  name: "Blog",
  head() {
    let name_ = this.blog.title;
    let title_ = name_
    let url_ = 'https://www.ragnarokmobile.net/guide/' + this.blog.slug
    let keywords_ = title_ + ', ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = this.blog.excerpt
    let image_ = this.blog.image
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
          hid: 'image',
          name: 'image',
          content: image_
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
          content: image_
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
        {
          hid: 'twitter:image',
          name: 'twitter:image',
          content: image_
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
      url: constant.url,
      loading: true,
      blog: [],
      slug: this.$route.params.slug
    };
  },
  methods: {
    getBlog() {
      axios
        .get(constant.getBlog + this.slug)
        .then(response => (this.blog = response.data))
        .catch(error => {})
        .finally(() => {
          this.loading = false;
        });
    }
  },
  async fetch() {
    await axios
    .get(constant.getBlog + this.slug)
    .then(response => (this.blog = response.data))
    .finally(() => this.loading = false)
  },
  fetchOnServer: true,
};
</script>
<style lang="scss">
.blog {
  p {
    font-size: 15px;
  }
  .body {
    img {
      object-fit: contain;
    }
  }
  ul {
    list-style: disc;
    padding-left: 24px !important;
    li:last-child {
      margin-bottom: 16px;
    }
  }
  .board_head {
    position: relative;
    margin: 0 auto 8px;
    padding: 13px 10px 0;
    .type {
      display: block;
      font-size: 12px;
      font-weight: 500;
      color: $primary;
      text-transform: uppercase;
      display: inline-flex;
      &:before {
        content: "#";
      }
    }
    .tit {
      display: block;
      padding-top: 6px;
      color: $primary;
      font-size: 22px;
      font-weight: 400;
      @media only screen and (max-width: 768px) {
        font-size: 20px;
      }
    }
    time {
      display: inline-flex;
      font-size: 12px;
      color: #6c7175;
      letter-spacing: 0.05em;
      margin-left: 5px;
      @media only screen and (max-width: 768px) {
        color: #6c7175;
        font-size: 10px;
      }
    }
  }
  .board_body {
    padding: 0 10px;
    font-size: 12px;
    img {
      max-width: 100%;
    }
  }
  .comments {
    padding: 0 10px;
  }
}
</style>