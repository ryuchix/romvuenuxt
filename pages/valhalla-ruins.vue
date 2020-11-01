<template>
  <div id="privacy">
    <v-app>
      <div class="content">
        <h2 class="mb-3">Valhalla Ruins (VR) Maps</h2>
        <p><strong>New Guild Instance</strong></p>
<p>- Silver Medal is not required for entering Guild Instance</p>
<p>- Restriction of minimum Guild Level 2 to enter Guild Instance is lifted</p>
<p>- 5 different levels of instances are combined into 1, and entry level is changed to 60</p>
<p>- The way to enter the dungeon remains the same. You can enter via Ruins Entrance in Guild. The guild teammates of the same team can enter the same dungeon through the entrance</p>
<p>- If the team got wiped, the dungeon will be reset, but the defeated Mini/MVP will not be refreshed</p>
<p>- Map contains normal monsters and 5 Mini/MVP. Defeating of Mini/MVP gives corresponding rewards. Rewards are account limited and only obtainable once per week</p>
<p>- Reward Adjustment: Rewards will be doubled for defeating Mini/MVP after optimization, and two random rewards on top of the double rewards will be given as well</p>

     
        <div class="comments">
          <div
            class="fb-like"
            style="margin-bottom: 5px;"
            data-href="https://www.ragnarokmobile.net/valhalla-ruins"
            data-layout="standard"
            data-action="like"
            data-size="small"
            data-show-faces="true"
            data-share="true"></div>
          <div class="pad30"></div>
          <div
            class="fb-comments"
            data-href="https://www.ragnarokmobile.net/valhalla-ruins"
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
    let title_ = "Valhalla Ruins Maps SEA and Global | Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/valhalla-ruins'
    let keywords_ = 'ragnarok mobile Vallhala ruins for SEA and GLobal, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Valhalla Ruins or Guild Ruins VR/GR is a dungeon quest for all members of the guild. The ruins consist of 5 doors, by default the portals are closed and you need Silver Medal to open it. Your need to reach a certain level to enter the dungeon, level 40, 60, 80, 100 and 120. Each door needs 40 silver medals. Unlike Endless Tower the VR/GR maps are the same across all Guilds in all channels.'
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