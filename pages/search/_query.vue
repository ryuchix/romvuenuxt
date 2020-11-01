<template>
  <div id="app">
    <div class="content">
      <div v-if="
       monsters == null && monsters.length == 0 && 
       equipments == null && equipments.length == 0 && 
       items == null &&  items.length == 0 && 
       cards == null && cards.length == 0 && 
       furnitures == null && furnitures.length == 0 && 
       headwears == null && headwears.length == 0 && 
       pets == null && pets.length == 0 && 
       pets == null && blogs.length == 0 && !loading ">
          <h2>No results found!</h2>
      </div>
      <div class="monsters-container mb-3" v-if="monsters != null && monsters.length > 0">
        <h2>Monsters</h2>
        <div
          v-for="monster in monsters"
          :key="monster.id"
          class="monsters">
          <div class="d-flex">

          <nuxt-link :to="{ name: 'monster-slug', params: { slug: monster.slug }}">
            <div class="monster-details">
              <div class="monster-image pointer" :class="monster.star != 'star' ? monster.type : 'star'">
                <img :src="monster.icon" :alt="monster.name_en" />
              </div>
            </div>
          </nuxt-link>
            <div class="monster-info">
              <nuxt-link :to="{ name: 'monster-slug', params: { slug: monster.slug }}">
              <div class="monster-name pointer">{{ monster.name_en }}</div>
              </nuxt-link>
              <div class="monster-attr">
                <div class="monster-stats_">
                  {{ monster.element }}
                  <span>·</span>
                  {{ monster.race }}
                  <span>·</span>
                  {{ monster.size }}
                </div>
                <div class="monster-stats">
                  Lv:
                  <strong>{{ monster.level }}</strong>
                  <span>·</span> HP:
                  <strong>{{ formatNumber(monster.hp) }}</strong>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="equipments-container mb-3" v-if="cards != null && cards.length > 0">
        <h2>Cards</h2>
        <div class="equipments" v-for="item in cards" :key="item.id">
          <nuxt-link :to="{ name: 'card-slug', params: { slug: item.slug }}">
            <div class="equipment-details clearfix">
              <div class="image">
                <img src="@/assets/images/defaultcardimg.png" :alt="item.name_en" />
              </div>
            </div>
          </nuxt-link>
          <div class="equipment-info">
            <nuxt-link :to="{ name: 'card-slug', params: { slug: item.slug }}">
              <div class="equipment-name">{{ item.name_en }}</div>
            </nuxt-link>
            <div class="equipment-attr">
              <div class="equipment-type_">{{ item.type_name }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="equipments-container mb-3" v-if="equipments != null && equipments.length > 0">
        <h2>Equipments</h2>
        <div class="equipments" v-for="equipment in equipments" :key="equipment.id">
          <nuxt-link :to="{ name: 'equipment-slug', params: { slug: equipment.slug }}">
            <div class="equipment-details clearfix">
              <div class="image">
                <img :src="equipment.icon" :alt="equipment.name_en" />
              </div>
            </div>
          </nuxt-link>
          <div class="equipment-info">
            <nuxt-link :to="{ name: 'equipment-slug', params: { slug: equipment.slug }}">
              <div class="equipment-name">{{ equipment.name_en }}</div>
            </nuxt-link>
            <div class="equipment-attr">
              <div class="equipment-type_">{{ equipment.type_name }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="equipments-container mb-3" v-if="items != null && items.length > 0">
        <h2>Items</h2>
        <div class="equipments" v-for="item in items" :key="item.id">
          <nuxt-link :to="{ name: 'item-slug', params: { slug: item.slug }}">
            <div class="equipment-details clearfix">
              <div class="image" :class="item.type_name == 'Blueprint' ? 'blueprint' : (item.type_name == 'Furniture Blueprint' ? 'fblueprint' : '')">
                <img :src="item.icon" :alt="item.name_en" />
              </div>
            </div>
          </nuxt-link>
          <div class="equipment-info">
            <nuxt-link :to="{ name: 'item-slug', params: { slug: item.slug }}">
              <div class="equipment-name">{{ item.name_en }}</div>
            </nuxt-link>
            <div class="equipment-attr">
              <div class="equipment-type_">{{ item.type_name }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="equipments-container mb-3" v-if="headwears != null && headwears.length > 0">
        <h2>Headwears</h2>
        <div class="equipments" v-for="item in headwears" :key="item.id">
          <nuxt-link :to="{ name: 'headwear-slug', params: { slug: item.slug }}">
            <div class="equipment-details clearfix">
              <div class="image">
                <img :src="item.icon" :alt="item.name_en" />
              </div>
            </div>
          </nuxt-link>
          <div class="equipment-info">
            <nuxt-link :to="{ name: 'headwear-slug', params: { slug: item.slug }}">
              <div class="equipment-name">{{ item.name_en }}</div>
            </nuxt-link>
            <div class="equipment-attr">
              <div class="equipment-type_">{{ item.type_name }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="equipments-container mb-3" v-if="furnitures != null && furnitures.length > 0">
        <h2>Furnitures</h2>
        <div class="equipments" v-for="item in furnitures" :key="item.id">
          <nuxt-link :to="{ name: 'furniture-slug', params: { slug: item.slug }}">
            <div class="equipment-details clearfix">
              <div class="image">
                <img :src="item.icon" :alt="item.name_en" />
              </div>
            </div>
          </nuxt-link>
          <div class="equipment-info">
            <nuxt-link :to="{ name: 'furniture-slug', params: { slug: item.slug }}">
              <div class="equipment-name">{{ item.name_en }}</div>
            </nuxt-link>
            <div class="equipment-attr">
              <div class="equipment-type_">{{ item.type_name }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="equipments-container mb-3" v-if="pets != null && pets.length > 0">
        <h2>Pets</h2>
        <div class="equipments" v-for="item in pets" :key="item.id">
          <nuxt-link :to="{ name: 'pet-slug', params: { slug: item.slug }}">
            <div class="equipment-details clearfix">
              <div class="image">
                <img style="object-fit: contain; padding: 0px" :src="item.icon" :alt="item.name" />
              </div>
            </div>
          </nuxt-link>
          <div class="equipment-info">
            <nuxt-link :to="{ name: 'pet-slug', params: { slug: item.slug }}">
              <div class="equipment-name">{{ item.name }}</div>
            </nuxt-link>
            <div class="equipment-attr">
              <div class="equipment-type_">Pet</div>
            </div>
          </div>
        </div>
      </div>
      <div class="blogs-container mb-3" v-if="blogs.length > 0">
        <h2>Guides</h2>
        <div v-for="blog in blogs" :key="blog.id">
          <nuxt-link :to="{ name: 'guide-slug', params: { slug: blog.slug }}">
            {{ blog.title }}
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import { constant } from '@/plugins/Constant';

export default {
  name: "Search",
  components: {
    //
  },

  head() {
    let title_ = "Search results for " + this.query + " | Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/search/' + this.query
    let keywords_ = this.query + ' ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = "Search results for " + this.query + ' Your ultimate guide for Ragnarok Mobile Eternal Love. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
    let image_ = 'https://www.ragnarokmobile.net/img/louyang.webp'
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
      loading: false,
      results: [],
      query: this.$route.params.query,
      items: [],
      cards: [],
      equipments: [],
      blogs: [],
      monsters: [],
      headwears: [],
      pets: [],
      furnitures: [],
    };
  },
  methods: {
    getResults() {
      this.loading = true;
      this.results = [];
      axios
        .get(constant.getSearch + this.query)
        .then(response => {
          this.items = response.data.items;
          this.cards = response.data.cards;
          this.equipments = response.data.equipments;
          this.blogs = response.data.blogs;
          this.monsters = response.data.monsters;
          this.headwears = response.data.headwears;
          this.furnitures = response.data.furnitures;
          this.pets = response.data.pets;
        })
        .catch(error => console.log(error))
        .finally(() => (this.loading = false));
    },
    formatNumber(num) {
      if (num != null)
        return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
    }
  },
  mounted() {
    this.getResults();
  }
};
</script>
<style lang="scss">
.monsters-container {
  .monsters {
    margin-left: 7px;
    padding: 0;
    width: 100%;
    margin-bottom: 0;
    transition: 0.2s ease-in-out;
    padding: 8px 0;
    display: flex;
    border: 1px solid transparent;
    text-overflow: ellipsis;
    white-space: nowrap;
    flex-direction: row;
    align-items: center;
    border-bottom: 1px solid #e8ebf7;
    &:last-child {
      border-bottom: 0;
    }
    .monster-details {
      display: inline-block;
      line-height: 10px;
    }
    .col-12 {
      display: flex;
    }
    .monster-image {
      @include imagecontainer;
      &.mvp {
        &:after {
          background: url("../../assets/images/monster-icon-min.png") 0;
          background-repeat: no-repeat;
          position: absolute;
          top: -4px;
          left: -4px;
          background-size: 150px;
          content: "";
          width: 23px;
          height: 27px;
          background-position: 0 0;
        }
      }
      &.mini {
        &:after {
          background: url("../../assets/images/monster-icon-min.png") 0;
          background-repeat: no-repeat;
          position: absolute;
          top: -4px;
          left: -4px;
          background-size: 150px;
          content: "";
          width: 27px;
          height: 24px;
          background-position: -30px 0;
        }
      }
      &.star {
        &:after {
          background: url("../../assets/images/monster-icon-min.png") 0;
          background-repeat: no-repeat;
          position: absolute;
          top: 0px;
          left: auto;
          right: 0;
          background-size: 150px;
          content: "";
          width: 18px;
          height: 18px;
          background-position: 0 -30px;
        }
      }
      &.undead {
        &:after {
          background: url("../../assets/images/monster-icon-min.png") 0;
          background-repeat: no-repeat;
          position: absolute;
          top: -5px;
          left: -4px;
          background-size: 150px;
          content: "";
          width: 30px;
          height: 30px;
          background-position: -30px -26px;
        }
      }
    }
    img {
      @include imagecontainer_img;
      padding: 0px;
    }
    .monster-info {
      align-self: center;
      .monster-name {
        margin-left: 6px;
        font-size: 1.3em;
        font-weight: 500;
        color: $primary;
      }
      .monster-attr {
        color: $disabled;
        margin-left: 6px;
      }
      .monster-stats {
        color: $black;
        font-size: 1em;
      }
      .monster-stats_ {
        text-transform: uppercase;
        font-size: 0.9em;
      }
    }
  }
}

.equipments-container {
  .equipments {
    &:last-child {
      border-bottom: 0;
    }
  }
  .equipment-info {
    align-self: flex-start;
  }
  .image {
    &.blueprint {
        background: url('../../assets/images/blueprint.png');
        background-repeat: no-repeat;
        border: 2px solid #c6a460;
        background-size: cover;
    }
    &.fblueprint {
        background-color: #4b8ad5;
        border: 2px solid #4b8ad5;
    }
  }
.equipments {
    position: relative;
    overflow: hidden;
    padding: 10px;
    border-bottom: 1px solid $bordercolor;
    display: flex;
    .equipment-details {
        display: inline-block;
        line-height: 10px;
        .image {
            @include imagecontainer;
            img {
                @include imagecontainer_img;
            }
        }
        .equipment-type {
            position: relative;
            padding: 5px 0;
            text-align: center;
            color: $disabled;
            line-height: 1.2em;
        }
    }
    .equipment-info {
        align-self: center;
        .equipment-name {
            margin-left: 6px;
            font-size: 1.2em;
            font-weight: 500;
            color: $primary;
        }
        .equipment-attr {
            margin-left: 6px;
            .equipment-type_ {
                color: $accent;
                font-weight: 600;
                letter-spacing: 1px;
                text-transform: uppercase;
                font-size: 0.9em;
            }
        }
        .equipment-stats {
            margin-left: 2px;
            margin-top: 3px;
            ul {
                li {
                    font-size: 0.9em;
                    line-height: 1.5em;
                    color: $black;
                    position: relative;
                    padding-left: 14px;
                    &:before {
                        content: '';
                        position: absolute;
                        left: 0;
                        width: 0;
                        height: 0;
                        margin-top: 6px;
                        width: 0;
                        height: 0;
                        border-style: solid;
                        border-width: 5px 0 5px 7px;
                        border-color: transparent transparent transparent $accent;
                    }
                }
            }
        }
    }
}
}
</style>