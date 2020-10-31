<template>
  <div id="privacy">
    <v-app>
      <div class="content">
        <h2 class="mb-3">Endless Tower SEA (ET)</h2>
        <p>Endless Tower resets every Monday at 6PM GMT+8 on SEA and Global Server. Selected floors consists of MVPS and Mini bosses and they are based on the last digit of the channel you are in. Example, if you are in PH25, all channels that ends in 5 like 5, 15, 25, 35 etc will have the same monsters.</p>
        <h3>{{ result.date }}</h3>
        <img :src="result.et" alt="Endless Tower MVP" style="width: 100%;"> <br><br>
        <img v-if="result.etmini != 0" :src="result.etmini" alt="Endless Tower Mini" style="width: 100%;">
        <br><br>
        <h2 class="mb-3">Valhalla Ruins (VR) Maps</h2>
        <p>Valhalla Ruins or Guild Ruins VR/GR is a dungeon quest for all members of the guild. The ruins consist of 5 doors, by default the portals are closed and you need Silver Medal to open it. Your need to reach a certain level to enter the dungeon, level 40, 60, 80, 100 and 120. Each door needs 40 silver medals. Unlike Endless Tower the VR/GR maps are the same across all Guilds in all channels.</p>
        <h3>{{ result.date }}</h3>
        <img :src="result.vr" alt="Valhalla Ruins Maps" style="width: 100%;">
        <br><br>
        <div v-if="result.etglobal != 0">
          <h2 class="mb-3">Endless Tower Global (ET)</h2>
          <p>Endless Tower resets every Monday at 6PM GMT+8 on SEA and Global Server. Selected floors consists of MVPS and Mini bosses and they are based on the last digit of the channel you are in. Example, if you are in PH25, all channels that ends in 5 like 5, 15, 25, 35 etc will have the same monsters.</p>
          <h3>{{ result.date }}</h3>
          <img :src="result.etglobal" alt="Endless Tower Global MVP" style="width: 100%;"> <br><br>
          <img v-if="result.etglobalmini != 0" :src="result.etglobalmini" alt="Endless Tower Global Mini" style="width: 100%;">
        </div>
        <br><br>
        <p><em>Images are not ours. Credit to original uploader. Thanks</em></p>
        <div class="comments">
          <div
            class="fb-like"
            style="margin-bottom: 5px;"
            data-href="https://ragnarokmobile.net/endless-tower"
            data-layout="standard"
            data-action="like"
            data-size="small"
            data-show-faces="true"
            data-share="true"></div>
          <div class="pad30"></div>
          <div
            class="fb-comments"
            data-href="https://ragnarokmobile.net/endless-tower"
            data-numposts="5"
            data-width="100%"></div>
        </div>
      </div>
    </v-app>
  </div>
</template>
<script>
import axios from "axios";
import { constant } from "@/plugins/Constant";

export default {
  name: "EndlessTower",
  layout: 'default',
  head() {
    let title_ = "Endless Tower SEA and Global| Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/endless-tower'
    let keywords_ = 'ragnarok mobile endless tower SEA and Global, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Endless Tower Floor Monsters List, Endless Tower SEA Global MVP, Endless Tower Mini. Endless Tower resets every Monday at 6PM GMT+8 on SEA Server.'
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
    this.getResults();
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