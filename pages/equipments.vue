<template>
    <div class="content" v-if="!loading">
      <div class="filters d-flex flex-row justify-center justify-space-around">
        <div class="all-races">
          <v-menu z-index="9" max-height="300" bottom offset-y :close-on-click="closeOnClick">
            <template v-slot:activator="{ on, attrs }">
              <span class="v-btn__content" 
                v-bind="attrs"
                v-on="on">Jobs<v-icon>mdi-menu-down</v-icon></span>
            </template>
            <v-list tile dense flat min-width="100" >
              <v-list-item light link v-for="(job, index) in jobs" :key="index"
                :class="$route.query.job == job ? '_active' : ''"
                @click="$router.push({name: 'equipments', query: query({job: job})})">
                <v-list-item-title dense>{{ job }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
        <div class="all-elements">
          <v-menu max-height="300" bottom offset-y :close-on-click="closeOnClick">
            <template v-slot:activator="{ on, attrs }">
              <span class="v-btn__content" 
                v-bind="attrs"
                v-on="on">Position<v-icon>mdi-menu-down</v-icon></span>
            </template>
            <v-list tile dense min-width="100">
              <v-list-item link v-for="(position, index) in positions" :key="index"
                :class="$route.query.position == position ? '_active' : ''"
                @click="$router.push({name: 'equipments', query: query({position: position})})">
                <v-list-item-title dense>{{ position }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
        <div class="all-sizes">
          <v-menu :disabled="menuDisabled" max-height="300" bottom offset-y :close-on-click="closeOnClick">
            <template v-slot:activator="{ on, attrs }">
              <span class="v-btn__content" 
                v-bind="attrs"
                v-on="on">Weapon Type<v-icon>mdi-menu-down</v-icon></span>
            </template>
            <v-list tile dense min-width="100">
              <v-list-item link v-for="(type, index) in weapon_types" :key="index"
                :class="$route.query.type == type ? '_active' : ''"
                @click="$router.push({name: 'equipments', query: query({type:type})})">
                <v-list-item-title>{{ type }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
      </div>
         <div class="equipments mt-7" v-for="equipment in equipments" :key="equipment.id">
           <nuxt-link :to="{ name: 'equipment-slug', params: { slug: equipment.slug }}" >
            <div class="equipment-details clearfix">
                <div class="image">
                    <img :src="equipment.icon" :alt="equipment.name_en">
                </div>
            </div>
            </nuxt-link>
            <div class="equipment-info">
              <nuxt-link :to="{ name: 'equipment-slug', params: { slug: equipment.slug }}" >
                <div class="equipment-name">{{ equipment.name_en }}</div>
                </nuxt-link>
                <div class="equipment-attr">
                    <div class="equipment-type_">
                        {{ equipment.type_name }}
                    </div>
                    <div class="equipment-stats">
                       <ul>
                           <li v-for="stat in equipment.stat" :key="stat">{{ stat }}</li>
                           <li v-for="o_stat in equipment.stat_extra" :key="o_stat">{{ o_stat }}</li>
                        </ul>
                    </div>
                </div>
            </div>
            
         </div>
        <infinite-loading v-if="!loading" spinner="waveDots" @infinite="loadmore">
            <div slot="no-more">End</div>          
        </infinite-loading>
    </div>
    
</template>

<script>
import axios from 'axios'
import { constant } from '@/plugins/Constant';
import InfiniteLoading from 'vue-infinite-loading';

export default {
  name: 'Equipments',
  components: {
    InfiniteLoading
  },
  head() {
    let title_ = "Ragnarok equipments database, equipments drop, item synthesis, item tiers for Ragnarok Mobile Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/equipments'
    let keywords_ = 'Ragnarok equipments database, equipments drop, item synthesis, item tiers, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Browse the Ragnarok Mobile equipments, items, weapons, armors and other gears database. Your ultimate guide for Ragnarok Mobile Eternal Love. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
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
      equipments: [],
      page: 2,
      menuDisabled: true,
      closeOnClick: true,
      jobs: [
        'All',
        'Advanced Novice',
        'Alchemist',
        'Assassin',
        'Bard',
        'Blacksmith',
        'Crusader',
        'Dancer',
        'Doram',
        'Hunter',
        'Knight',
        'Monk',
        'Priest',
        'Rouge',
        'Sage',
        'Wizard'],
      positions: [
        'All',
        'Off-hand',
        'Armor',
        'Garment',
        'Footgear',
        'Accessory',
        'Weapon'
      ],
      weapon_types: [
        'All',
        'Spear',
        'Sword',
        'Staff',
        'Katar',
        'Bow',
        'Mace',
        'Axe',
        'Book',
        'Dagger',
        'Musical Instrument',
        'Whips',
        'Knuckles'
      ],
      q: this.$route.query,
      fquery: this.$route.fullPath.replace("/equipments", "")
    }
  },
  methods: {
    query(newQuery) {
      if (this.$route.query.position == 'Weapon') {
        this.menuDisabled = false
      } else {
        this.menuDisabled = true
      }
      return {
        ...this.$route.query,
        ...newQuery
      }
    },
    filterEquipments() {
      axios
        .get(constant.filterEquipments + this.fquery)
        .then(response => (this.equipments = response.data.data))
        .catch(error => console.log(error))
        .finally(() => this.loading = false)
    },
    getEquipments() {
      axios
        .get(constant.getEquipments)
        .then(response => (this.equipments = response.data.data))
        .catch(error => console.log(error))
        .finally(() => this.loading = false)
    },
    loadmore($state) {
      let vm = this;
      if(Object.entries(this.$route.query).length === 0) {
        axios
          .get(constant.getEquipments+'?page='+vm.page)
          .then(response => {
            response.data.data.map(function(value) {
                vm.equipments.push(value);
            });
            if ((vm.page - 1) == response.data.last_page) {
              $state.complete();
            }
            vm.page += 1;
            $state.loaded();
          })
          .catch(error => console.log(error))
          .finally(() => console.log())
      } else {
        axios
          .get(constant.filterEquipments + vm.fquery +'&page='+vm.page)
          .then(response => {
            response.data.data.map(function(value) {
                vm.equipments.push(value);
            });
            if ((vm.page - 1) == response.data.last_page) {
              $state.complete();
            }
            vm.page += 1;
            $state.loaded();
          })
          .catch(error => console.log(error))
          .finally(() => console.log())
      }
    },
    formatNumber(num) {
      return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
    }
  },
  mounted () {
    this.menuDisabled = this.$route.query.position != 'Weapon'
    if (Object.entries(this.$route.query).length === 0) {
      this.getEquipments();
    } else {
      this.filterEquipments();
    }
  },
  computed: {
      nonNullItems: function() {
          return this.items.filter(function(item) {
          return item !== null;
          });
      }
  }
}
</script>
<style lang="scss" scoped>
  .equipments {
    a {
      height: fit-content;
    }
    ._active {
      background-color: #eee;
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
</style>
