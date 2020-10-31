<template>
  <div>    
    <div class="content" v-if="!loading">
        <div class="single monster">
            <div class="single-row">
                <div class="image-container">
                    <div class="image">
                        <img :src="monster.icon" :alt="monster.name">
                    </div>
                    <div :class="'star-'+ monster.star"></div>
                </div>
                <div class="title-container">
                    <div class="title-container-inner">
                        <div class="item-title">
                            <h2>{{ monster.name }}</h2>
                        </div>
                        <div class="item-title-info">
                            <div class="type">
                                <nuxt-link :to="{ name: 'pets', query: { element: monster.element }}">{{ monster.element }}</nuxt-link> <span> · </span>
                                <nuxt-link :to="{ name: 'pets', query: { race: monster.race }}">{{ monster.race }}</nuxt-link><span> · </span>
                                <nuxt-link :to="{ name: 'pets', query: { size: monster.size }}">{{ monster.size }}</nuxt-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="description" v-if="monster.description != null && monster.description != ''">
                <div class="inner-description">{{ monster.description }}</div>
            </div>

        <div>
          <div v-if="monster.unlock != null && monster.unlock != ''">
            <div class="card-type__">Unlock</div>
            <div class="card-stats unlock">{{ monster.unlock }}</div>
          </div>
          <div v-if="monster.food != null">
            <div class="card-type__">Taming item</div>
            <nuxt-link :to="{ name: 'item-slug', params: { slug: monster.food.slug }}">
                <div v-ripple class="card-stats unlock"><img :src="monster.food.icon" :alt="monster.food.name_en"> {{ monster.food.name_en }}</div>
            </nuxt-link>
          </div>
          <div v-if="monster.safe != null">
            <div class="card-type__">100% catch rate</div>
            <div class="unlock">{{ monster.safe }} x <img :src="monster.food.icon" :alt="monster.food.name_en"> {{ monster.food.name_en }}</div>
          </div>
          <div v-if="monster.compose != null && monster.compose.length > 0">
            <div class="card-type__">Pet Fusion</div>
            <div class="pet-fusion">
              <div class="dropped">
                <div v-for="mons in monster.compose" :key="mons.id" class="monsters row no-gutters">
                    <div class="col-sm-12 col-12">
                        <div class="monster-details">
                            <div class="monster-image">
                                <img :src="mons.icon" :alt="mons.name">
                            </div>
                        </div>
                        <div class="monster-info">
                            <nuxt-link :to="{ name: 'pet-slug', params: { slug: mons.slug }}" class="d-flex">
                              <div class="monster-name">{{ mons.name }}</div>
                            </nuxt-link>
                        </div>
                    </div>
                </div>
              </div>
            </div>
          </div>
        </div>


            <div v-if="monster.skills != null && monster.skills.length > 0">
                <div class="sub-heading clear">
                    <h3>Skills</h3>
                </div>
                <div class="drops">
                <div class="attr">
                    <ul>
                        <li v-for="skill in monster.skills" :key="skill.id">
                            <strong>{{ skill.name }}</strong> <span class="skilllvl">(Lvl. {{ skill.lvl }})</span>
                            <div class="skilldesc" v-html="skill.description"> </div>
                        </li>
                    </ul>
    
                    </div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { constant } from '@/plugins/Constant';

export default {
  name: 'Pet',
  components: {
    //
  },

  head() {
    let name_ = this.monster.name;
    let title_ = name_ + ', How to get ' + name_ + '. Pet Fusion, Taming Item, How to catch 100% success rate in Ragnarok Mobile'
    let url_ = 'https://www.ragnarokmobile.net/pet/' + this.monster.slug
    let keywords_ = 'Ragnarok monsters database, monsters drop, monsters location, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Get ' + name_ + ' information and attributes, pet fusion, taming item, how to catch 100% success rate. Your ultimate guide for Ragnarok Mobile Eternal Love. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
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
        id: this.$route.params.slug,
        loading: true,
        monster: {},
        fullPage: false,
    }
  },
  created () {
    this.getMonsters()
  },
  methods:  {
    getMonsters() {
      axios
        .get(constant.getPet+this.id)
        .then(response => (this.monster = response.data))
        .catch(error => console.log(error))
        .finally(() => this.loading = false)
    },
    formatNumber(num) {
        if (num != null) return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
    }
  }
}
</script>
<style lang="scss">
    em {
        font-weight: 500;
    }
    .skilllvl {
        color: $disabled;
        font-size: 0.8em;
    }
    .skilldesc {
        margin-left: -15px;
        font-size: 0.9em;
    }
    .unlock {
        margin-left: 6px;

        img {
            width: 20px;
            height: 20px;
        }
    }

.monster {
    display: inline-block;
    width: 100%;
    clear: both;
    padding: 5px;
    .single-row {
        display: flex;
        .image-container {
            float: left;
            width: 60px;

            .star-1 {
                width: 10px;
                height: 11px;
                margin: 1px 33px 0;
                background: url('../../assets/images/star.png') -10px -1px;
                background-repeat: no-repeat;
            }
            .star-2 {
                width: 20px;
                height: 11px;
                margin: 1px 27px 0;
                background: url('../../assets/images/star.png') -10px -1px;
                background-repeat: no-repeat;
            }
            .star-3 {
                width: 30px;
                height: 11px;
                margin: 1px 24px 0;
                background: url('../../assets/images/star.png') -10px -1px;
                background-repeat: no-repeat;
            }
            .star-4 {
                width: 40px;
                height: 11px;
                margin: 1px 21px 0;
                background: url('../../assets/images/star.png') -10px -1px;
                background-repeat: no-repeat;
            }
            
        }
        .image {
            @include imagecontainer;           
            &.mvp {
                &:after {
                    background: url('../../assets/images/monster-icon-min.png') 0;
                    background-repeat: no-repeat;
                    position: absolute;
                    top: -4px;
                    left: -4px;
                    background-size: 150px;
                    content: '';
                    width: 23px;
                    height: 27px;
                    background-position: 0 0;
                }
            }
            &.mini {
                &:after {
                    background: url('../../assets/images/monster-icon-min.png') 0;
                    background-repeat: no-repeat;
                    position: absolute;
                    top: -4px;
                    left: -4px;
                    background-size: 150px;
                    content: '';
                    width: 27px;
                    height: 24px;
                    background-position: -30px 0;
                }
            }
            &.star {
                &:after {
                    background: url('../../assets/images/monster-icon-min.png') 0;
                    background-repeat: no-repeat;
                    position: absolute;
                    top: 0px;
                    left: auto;
                    right: 0;
                    background-size: 150px;
                    content: '';
                    width: 18px;
                    height: 18px;
                    background-position: 0 -30px;
                }
            }
            &.undead {
                &:after {
                    background: url('../../assets/images/monster-icon-min.png') 0;
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
        .item-title {
            text-transform: capitalize;
            font-weight: 500;
            h2 {
                font-size: 1.3em;
                padding: 2px .9em;
                overflow: hidden;
                color: $primary;
            }
        }
        .item-title-info {
            display: inline-block;
            margin: 0 1.2em;
            .type {
                color: $primary;
                text-overflow: ellipsis;
                text-transform: uppercase;
                font-size: .9em;
                
            }
        }
    }

    .description {
        display: flex;
        margin: 1em 0;
        padding: 10px;
        background: $backgroundcolor;
        border-radius: 2px;
        .inner-description {
            font-size: 0.9em;
            letter-spacing: 1;
        }
    }

    .sub-heading {
        width: 100%;
        padding: 5px;
        border-radius: 2px;
        text-transform: uppercase;
        font-weight: 600;
        color: $primary;
        font-size: 0.9em;
    }

    .attr {
        overflow: hidden;
        position: relative;
        margin-top: 10px;
        border: 1px solid $bordercolor;
        border-radius: 5px;
        dl {
            overflow: hidden;
            position: relative;
            float: left;
            width: 50%;
            padding: 7px 0;
            border-top: 1px solid $bordercolor;
            &:first-child {
                border-top: none;
            }
        }
        dt {
            float: left;
            width: 6em;
            text-indent: 10px;
        }
        dd {
            overflow: hidden;
            color: $secondary;
        }
        .full {
            float: none;
            width: auto;
        }
    }
    .drops {
        .attr {
            border: 0px;
            border-radius: 0px;

            ul {
                margin-left: 6px;
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
        dl {
            border-top: 0px solid $bordercolor;
            width: 100%;
            border-bottom: 1px solid $bordercolor;
            &:hover {
                background-color: $backgroundcolor;
                color: $primary;
            }
        }
        dt {
            width: auto;
            display: flex;
        }
        .item-info {
            display: flex;
            align-items: center;
            span {
                background-color: #e8ebf7;
                border: 1px #ccc solid;
                border-radius: 5px;
                margin-left: 5px;
                padding-right: 5px;
            }
        }
        .image {
            display: inline-block;
            line-height: 10px;
            img {
                height: 30px;
                width: 30px;
            }
        }
        .item-name {
            display: flex;
            text-overflow: ellipsis;
            width: 100%;
        }
        
    }
    .location {
        ul {
            margin-left: 5px;
        }
    }

    .card-type__ {
        margin-left: 6px;
        margin-top: 5px;
        margin-bottom: 5px;
        color: $accent;
        font-size: .9em;
        font-weight: 600;
        letter-spacing: 1px;
        text-transform: uppercase;
    }


    .pet-fusion {
        .dropped {
            .monsters {
                padding: 0;
                width: 100%;
                margin-bottom: 0;
                transition: .2s ease-in-out;
                padding: 2px;
                display: flex;
                border: 1px solid transparent;
                text-overflow: ellipsis;
                white-space: nowrap;
                flex-direction: row;
                align-items: center;
                &:hover {
                    background-color: $backgroundcolor;
                }
                .monster-details {
                    display: inline-block;
                    line-height: 10px;
                }
                .col-12 {
                    display: flex;
                }
                .monster-image {
                    width: 42px !important;
                    height: 42px !important;
                    @include imagecontainer;
                    border: 1px solid #abd2f3;
                }
                img {                
                    border: 1px solid $white !important;
                    width: 40px !important;
                    height: 40px !important;
                @include imagecontainer_img;
                padding: 0px;
                }
                .monster-info {
                    align-self: center;
                    .monster-name {
                        margin-left: 6px;
                        font-size: 1em;
                        font-weight: 500;
                        color: $primary;
                    }
                    .monster-attr {
                        color: $disabled;
                        margin-left: 6px;
                        font-size: 0.7em;
                        margin-top: -5px;
                    }
                }
            }
        }
    }
}
</style>
