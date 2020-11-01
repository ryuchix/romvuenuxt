
<template>
  <div id="privacy">
    <v-app>
      <div class="content">
        <h2 class="mb-3">Safe Refining Guide</h2>
        <p>Safe refining is the safest way to upgrade or refine your equipments to +10, however this method requires more copy of the item you want to refine, Oridecon/Elunium, and zeny to succefully achieve the refine you want. Please refer to the table below. </p>
          <v-simple-table dense>
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left"><strong>From</strong></th>
                  <th class="text-left"><strong>To</strong></th>
                  <th class="text-left"><strong>Same Equipment</strong></th>
                  <th class="text-left"><strong>Oridecon/Elunium</strong></th>
                  <th class="text-left"><strong>Zeny</strong></th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>4</td>
                  <td>5</td>
                  <td>1</td>
                  <td>5</td>
                  <td>100,000</td>
                </tr>
                <tr>
                  <td>5</td>
                  <td>6</td>
                  <td>2</td>
                  <td>10</td>
                  <td>220,000</td>
                </tr>
                <tr>
                  <td>6</td>
                  <td>7</td>
                  <td>3</td>
                  <td>15</td>
                  <td>470,000</td>
                </tr>
                <tr>
                  <td>7</td>
                  <td>8</td>
                  <td>4</td>
                  <td>25</td>
                  <td>910,000</td>
                </tr>
                <tr>
                  <td>8</td>
                  <td>9</td>
                  <td>6</td>
                  <td>50</td>
                  <td>1,630,000</td>
                </tr>
                <tr>
                  <td>9</td>
                  <td>10</td>
                  <td>10</td>
                  <td>85</td>
                  <td>2,740,000</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>    
          <br> 


        <div class="comments">
          <div
            class="fb-like"
            style="margin-bottom: 5px;"
            data-href="https://www.ragnarokmobile.net/safe-refining-guide"
            data-layout="standard"
            data-action="like"
            data-size="small"
            data-show-faces="true"
            data-share="true"></div>
          <div class="pad30"></div>
          <div
            class="fb-comments"
            data-href="https://www.ragnarokmobile.net/safe-refining-guide"
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
  name: "SafeRefine",

  head() {
    let title_ = "Safe Refine Guide | Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love"
    let url_ = 'https://ragnarokmobile.net/safe-refine-guide'
    let keywords_ = 'Safe refine, safe refining, safe refining costs, total costs, tricks, tips, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Safe refining guide to make yo'
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
        loading: true,
        result: [],
    }
  },
  mounted() {
    //
  },
  methods: {
    getResults() {
      this.loading = true;
      axios
        .get(constant.getWeeklies)
        .then(response => {
          this.result = response.data;
        })
        .catch(error => console.log(error))
        .finally(() => (this.loading = false));
    },
  }
};
</script>