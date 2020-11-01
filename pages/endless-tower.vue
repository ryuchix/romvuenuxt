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
        <p><strong>New Guild Instance</strong></p>
<p>- Silver Medal is not required for entering Guild Instance</p>
<p>- Restriction of minimum Guild Level 2 to enter Guild Instance is lifted</p>
<p>- 5 different levels of instances are combined into 1, and entry level is changed to 60</p>
<p>- The way to enter the dungeon remains the same. You can enter via Ruins Entrance in Guild. The guild teammates of the same team can enter the same dungeon through the entrance</p>
<p>- If the team got wiped, the dungeon will be reset, but the defeated Mini/MVP will not be refreshed</p>
<br>
<p>- Map contains normal monsters and 5 Mini/MVP. Defeating of Mini/MVP gives corresponding rewards. Rewards are account limited and only obtainable once per week</p>
<p>- Reward Adjustment: Rewards will be doubled for defeating Mini/MVP after optimization, and two random rewards on top of the double rewards will be given as well</p>

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