<template>
  <div>    
    <div class="content" v-if="!loading">
        <div class="single card">
            <div class="single-row">
                <div class="image-container">
                    <div class="image">
                        <img :src="card.icon" :alt="card.name_en" />
                    </div>
                </div>
                <div class="title-container">
                    <div class="title-container-inner">
                        <div class="item-title">
                            <h2>{{ card.name_en }}</h2>
                        </div>
                        <div class="item-title-info">
                            <div class="type">{{ card.type_name }}</div>
                        </div>
                        <div class="item-tags">
                            <div class="tag" :class="card.tradable ? 'enable' : 'disable'">
                                <i aria-label="tradable" class="material-icons">{{ card.tradable ? 'check' : 'close' }}</i> Trade
                            </div>
                            <div class="tag" :class="card.compose_recipe != 0 && card.compose.length > 0 ? 'enable' : 'disable'">
                                <i aria-label="craftable" class="material-icons">{{ card.compose_recipe != 0  && card.compose.length > 0 ? 'check' : 'close' }}</i> Craft
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="sub-heading">
                <h3>Attributes</h3>
            </div>
            <div class="card-stats">
                <ul>
                    <li v-for="(eff, index) in card.stat" :key="index">{{ eff }}</li>
                </ul>
            </div>
            <div class="card-type__">
                Unlock
            </div>
            <div class="card-stats unlock">
                {{ card.unlock_effect }}
            </div>
            <div class="card-type__">
                Deposit
            </div>
            <div class="card-stats deposit">
                {{ card.deposit_effect }}
            </div>

            <div v-if="card.monsters != null && card.monsters.length > 0">
                <div class="sub-heading clear">
                    <h3>Dropped by</h3>
                </div>
                <div class="dropped">
                <div class="row no-gutters">
                    <div class=" monsters col-sm-12 col-12" v-for="mons in card.monsters" :key="mons.id">
                        <div class="monster-details">
                            <div class="monster-image" :class="mons.star != 'star' ? mons.type : 'star'">
                                <img :src="mons.icon" :alt="mons.name_en">
                            </div>
                        </div>
                        <div class="monster-info">
                            <nuxt-link :to="{ name: 'monster-slug', params: { slug: mons.slug }}">
                              <div class="monster-name pointer">{{ mons.name_en }}</div>
                            </nuxt-link>
                            <div class="monster-attr">
                                <div class="monster-stats_">
                                    {{ mons.element }}<span> · </span>
                                    {{ mons.race }}<span> · </span>
                                    {{ mons.size }}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                </div>
            </div>

          <div v-if="card.compose_recipe == 1 && card.compose.length > 0">
            <div class="sub-heading clear">
                <h3>Craft</h3>
            </div>
            <div class="tiers">
              <v-expansion-panels accordion class="accordion" flat="flat">
                <v-expansion-panel v-for="synth in card.compose" :key="synth.id">
                  <v-expansion-panel-header>
                    <div class="attr" style="border: 0; margin-top: 0px;">
                    <dl>
                      <dd class="single-row" style="padding-left: 10px; font-size: 1em; align-items: center;">
                        <div class="image">
                          <img src="@/assets/images/defaultcardimg.png" :alt="synth['item_output']">
                        </div>
                        {{ synth['item_output'] }}
                      </dd>
                    </dl>
                    </div></v-expansion-panel-header>
                  <v-expansion-panel-content>
                    <div v-for="equip in synth.materials" :key="equip.id">
                      <div class="item-info" v-if="equip.item_id != null">
                          <div class="image is-24x24" :class="equip.item_id['type_name'] == 'Blueprint' ? 'blueprint' : ''">
                              <img v-if="equip.item_id['type'] != 'cards'" :src="equip.item_id['icon'] != null ? equip.item_id['icon'] : '' " :alt="equip.item_id['name_en'] != null ? equip.item_id['name_en'] : ''">
                              <img v-if="equip.item_id['type'] == 'cards'" src="@/assets/images/defaultcardimg.png" :alt="equip.item_id['name_en'] != null ? equip.item_id['name_en'] : ''">
                          </div>
                          <nuxt-link v-if="equip.item_id['type'] != 'cards'" :to="{ name: 'item-slug', params: { slug: equip.item_id['slug'] }}" style="line-height: 1.2em; display: flex;">
                              <div class="item-name">
                                  {{ equip.item_id['name_en'] }} x {{ equip.qty }}
                              </div>
                          </nuxt-link>
                          <nuxt-link v-if="equip.item_id['type'] == 'cards'" :to="{ name: 'card-slug', params: { slug: equip.item_id['slug'] }}" style="line-height: 1.2em; display: flex;">
                              <div class="item-name">
                                  {{ equip.item_id['name_en'] }} x {{ equip.qty }}
                              </div>
                          </nuxt-link>
                      </div>
                      <div class="item-info" v-else>
                         
                      </div>
                    </div>
                      <div class="item-info">
                          <div class="image is-24x24">
                              <img src="https://api.ragnarokmobile.net/uploads/items/100_img.png" alt="Zeny">
                          </div>
                          <nuxt-link :to="{ name: 'item-slug', params: { slug: 'zeny' }}" style="line-height: 1.2em; display: flex;">
                              <div class="item-name">
                                  {{ formatNumber(synth.cost) }} Zeny
                              </div>
                          </nuxt-link>
                      </div>
                  </v-expansion-panel-content>
                </v-expansion-panel>

              </v-expansion-panels>
            </div>
          </div>


        </div>

    </div>
  </div>
</template>

<script>
import axios from "axios";
import { constant } from '@/plugins/Constant';

export default {
  name: 'Card',
  components: {
    //
  },

  head() {
    let name_ = this.card.name_en;
    let title_ = name_ + ', ' + name_ + ' crafting requirements, where to get ' + name_ + ' who drops ' + name_ + ' in Ragnarok Mobile'
    let url_ = 'https://www.ragnarokmobile.net/card/' + this.card.slug
    let keywords_ = title_ + ', Ragnarok card database, card drop, ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
    let description_ = 'Get ' + name_ + ' information and attributes. Your ultimate guide for Ragnarok Mobile Eternal Love. Your source for Ragnarok M Monsters, Cards, Quests, Database, Headwears, Blueprints, Items, Market Prices, Exchange Price List and Stats and Skills calculator. ROM'
    let image_ = 'https://www.ragnarokmobile.net/img/louyang.webp';
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
      id: this.$route.params.slug,
      loading: true,
      card: {},
      fullPage: false
    }
  },
  methods: {
    formatNumber(num) {
      if (num != null)
        return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
    },
    getItem() {
      axios
        .get(constant.getCard + this.id)
        .then(response => (this.card = response.data))
        .catch(error => this.$router.replace({ name: "error" }))
        .finally(() => (this.loading = false));
    }
  },
  async fetch() {
    await axios
    .get(constant.getCard + this.id)
    .then(response => (this.card = response.data))
    .finally(() => this.loading = false)
  },
  fetchOnServer: true,
}
</script>
<style lang="scss">
.card {
  border: 0 !important;
}
.card {
    display: inline-block;
    width: 100%;
    clear: both;
    padding: 5px;
    .single-row {
        display: flex;
        .image-container {
            float: left;
            width: 60px;
        }
        .image {
            @include imagecontainer;
            width: 90px;
            height: 120px;
        }
        img {
           @include imagecontainer_img;
           width: 86px;
           height: 116px;
           padding: 0px;
           border: 0px solid #fff;
        }
        .item-title {
            margin: 0 1em;
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
            margin: 0 2.2em;
            .type {
                color: $accent;
                font-weight: 600;
                text-transform: uppercase;
                font-size: 0.9em;
                
            }
        }
        .item-tags {
            display: flex;
            margin: 5px 2.2em;
            .tag {
                display: flex;
                align-items: center;
                i {
                    font-size: 0.9em;
                }
                &.disable {
                    color: $disabled;
                }
                &.enable {
                    color: $accent;
                }
                background-color: $backgroundcolor;
                margin-right: 0.6em;
                padding: 0 5px;
                border: 1px solid $bordercolor;
                border-radius: 3px;
                font-size: 0.9em;
            }
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
    .card-stats {
        margin-left: 2px;
        margin-top: 3px;
        &.deposit {
            font-size: 0.9em;
            margin-top: -0.2em;
            margin-left: 6px;
        }
        &.unlock {
            font-size: 0.9em;
            margin-top: -0.2em;
            margin-left: 6px;
        }
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

    .sub-heading {
        width: 100%;
        padding: 5px;
        border-radius: 2px;
        text-transform: uppercase;
        font-weight: 600;
        color: $primary;
        font-size: 0.9em;
    }

    .attributes {
        margin-left: 7px;
        ul {
            li {
                font-size: 0.9em;
                line-height: 1.7em;
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
    .pill {
        li {
            display: inline-block;
            margin: 0 5px 5px 0;
            padding: 0 0.5em;
            border-radius: 1rem;
            background-color: $accent;
            font-size: 0.8rem;
            color: $white;
            &:hover {
                @include userselect;
                background-color: $primary
            }
        }
    }
    .accordion {
        border-radius: 0;
        .v-expansion-panel {
            border: 1px solid $bordercolor;
        }
        .v-expansion-panel-header__icon {
            margin-left: auto;
        }
        .v-expansion-panel-header--active {
            border-bottom: 1px solid $bordercolor;
            min-height: 48px;
        }
        .v-expansion-panel-content__wrap {
            padding: 10px 24px 16px;
        }
    }

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
                &.mvp {
                    &:after {
                        background: url('../../assets/images/monster-icon-min.png') 0;
                        background-repeat: no-repeat;
                        position: absolute;
                        top: -4px;
                        left: -4px;
                        background-size: 80px;
                        content: "";
                        width: 15px;
                        height: 15px;
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
                        background-size: 80px;
                        content: "";
                        width: 27px;
                        height: 14px;
                        background-position: -15px 0;
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
                        background-size: 80px;
                        content: "";
                        width: 18px;
                        height: 18px;
                        background-position: 8px -16px;
                    }
                }
                &.undead {
                    &:after {
                        background: url('../../assets/images/monster-icon-min.png') 0;
                        background-repeat: no-repeat;
                        position: absolute;
                        top: -5px;
                        left: -5px;
                        background-size: 80px;
                        content: "";
                        width: 32px;
                        height: 32px;
                        background-position: -15px -13px;
                    }
                }
            }
            img {                
                border: 1px solid $white !important;
                width: 40px !important;
                height: 40px !important;
               @include imagecontainer_img;
               padding: 0px;
            }
            .monster-info {
                align-self: end;
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

    .tiers {
        .accordion {
            border-radius: 0;
            .v-expansion-panel {
                border: 1px solid $bordercolor;
            }
            .v-expansion-panel-header {
                text-align: left;
                padding: 0 10px;
            }
            .v-expansion-panel-header__icon {
                margin-left: auto;
            }
            .v-expansion-panel-header--active {
                border-bottom: 1px solid $bordercolor;
                min-height: 48px;
            }
            .v-expansion-panel-content__wrap {
                padding: 10px 24px 16px;
            }
        }
        .attr {
            border: 0px;
            border-radius: 0px;
        }
        dl {
            border-top: 0px solid $bordercolor;
            width: 100%;
            padding: 2px 7px;
        }
        dt {
            width: auto;
            display: flex;
        }
        .item-info {
            display: flex;
            align-items: center;
        }
        .single-row {
            .image {
                border: 1px solid #abd2f3;
            }
        }
        .image {
            display: inline-block;
            line-height: 10px;
            margin-right: 10px;
            width: 27px;
            height: 27px;
            img {
                height: 25px;
                width: 25px;
                border: 1px solid #fff;
            }
    
            &.blueprint {
                background: url('../../assets/images/blueprint.png');
                background-repeat: no-repeat;
                border: 1px solid #c6a460;
                background-size: cover;
    
                img {
                    padding: 2px;
                    border: 1px solid $white;
                }
            }
        }
        .item-name {
            display: flex;
            text-overflow: ellipsis;
            width: 100%;
            font-size: 0.9em;
        }
    }

}
</style>
