<template>
    <div class="content" v-if="!loading">
        <div class="single equipment">
            <div class="single-row">
                <div class="image-container">
                    <div class="image" :class="equipment.type_name == 'Blueprint' ? 'blueprint' : (equipment.type_name == 'Furniture Blueprint' ? 'fblueprint' : '')">
                        <img :src="equipment.icon" :alt="equipment.name_en">
                    </div>
                </div>
                <div class="title-container">
                    <div class="title-container-inner">
                        <div class="item-title mb-1">
                            <h2>{{ equipment.name_en }}</h2>
                        </div>
                        <div class="item-title-info">
                            <div class="type">
                                {{ equipment.type_name }} {{ equipment.type_name == '- Blueprint' ? equipment.stat_type : '' }}
                            </div>
                        </div>
                        <div class="item-tags">
                            <div class="tag" :class="equipment.tradable ? 'enable' : 'disable'">
                                <i class="material-icons">{{ equipment.tradable ? 'check' : 'close' }}</i> Trade
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="description" v-if="equipment.desc_en != null">
                <div class="inner-description">
                    {{ equipment.desc_en }}
                </div>
            </div>
            <div v-if="equipment.type_name == 'Blueprint' && equipment.stat_extra != null && equipment.stat_extra.length != 0">
              <div class="sub-heading">
                  <h3>Attributes</h3>
              </div>
              <div class="attributes">
                <ul>
                  <li v-for="stat in equipment.stat" :key="stat">{{ stat }}</li>
                  <li v-for="extra in equipment.stat_extra" :key="extra">{{ extra }}</li>
                </ul>
              </div>
              <div v-if="equipment.unlock_effect != null || equipment.deposit_effect != null">
                <div v-if="equipment.unlock_effect != null">
                  <div class="card-type__">
                      Unlock
                  </div>
                  <div class="card-stats unlock">
                      {{ equipment.unlock_effect }}
                  </div>
                </div>
                <div v-if="equipment.deposit_effect != null">
                  <div class="card-type__">
                      Deposit
                  </div>
                  <div class="card-stats deposit">
                      {{ equipment.deposit_effect }}
                  </div>
                </div>   
              </div>
            </div>

            <div v-if="equipment.type_name == 'Blueprint'">
              <div class="attr clear">
                <dl v-if="equipment.compose_id != null && equipment.item_from != null && equipment.item_from['id'] != equipment.id">
                    <dt>Upgradable from</dt>
                    <dd class="single-row">
                      <div class="image">
                        <img :src="equipment.item_from['icon']" :alt="equipment.item_from['name_en']">
                      </div>
                      <nuxt-link :to="{ name: 'headwear-slug', params: { slug: equipment.item_from['slug'] }}"> {{ equipment.item_from['name_en'] }} </nuxt-link>
                    </dd>
                </dl>
                <dl v-if="equipment.compose_output_id != null && equipment.item_to != null">
                    <dt>Upgradable to</dt>
                    <dd class="single-row">              
                      <div class="image">
                        <img :src="equipment.item_to['icon']" alt="equipment.item_to['name_en']">
                      </div>
                      <nuxt-link :to="{ name: 'headwear-slug', params: { slug: equipment.item_to['slug'] }}"> {{ equipment.item_to['name_en'] }} </nuxt-link>
                      </dd>
                </dl>
              </div>
             </div>

            <div v-if="equipment.type_name == 'Furniture Blueprint'">
              <div class="attr clear">
                <dl v-if="equipment.compose_id != null && equipment.item_from != null && equipment.item_from['id'] != equipment.id">
                    <dt>Upgradable from</dt>
                    <dd class="single-row">
                      <div class="image">
                        <img :src="equipment.item_from['icon']" :alt="equipment.item_from['name_en']">
                      </div>
                      <nuxt-link :to="{ name: 'furniture-slug', params: { slug: equipment.item_from['slug'] }}"> {{ equipment.item_from['name_en'] }} </nuxt-link>
                    </dd>
                </dl>
                <dl v-if="equipment.compose_output_id != null && equipment.item_to != null">
                    <dt>Upgradable to</dt>
                    <dd class="single-row">              
                      <div class="image">
                        <img :src="equipment.item_to['icon']" alt="equipment.item_to['name_en']">
                      </div>
                      <nuxt-link :to="{ name: 'furniture-slug', params: { slug: equipment.item_to['slug'] }}"> {{ equipment.item_to['name_en'] }} </nuxt-link>
                      </dd>
                </dl>
              </div>
             </div>

            <div v-if="equipment.monsters != null && equipment.monsters.length > 0">
              <div class="sub-heading clear">
                  <h3>Dropped by</h3>
              </div>
              <div class="dropped">
                <div v-for="monster in equipment.monsters" :key="monster.id" class="monsters row no-gutters">
                    <div class="col-sm-12 col-12">
                        <div class="monster-details">
                            <div class="monster-image" :class="monster.star != 'star' ? monster.type : 'star'">
                                <img :src="monster.icon" :alt="monster.name_en">
                            </div>
                        </div>
                        <div class="monster-info">
                            <nuxt-link :to="{ name: 'monster-slug', params: { slug: monster.slug }}" class="d-flex">
                              <div class="monster-name">{{ monster.name_en }}</div>
                            </nuxt-link>
                            <div class="monster-attr">
                                <div class="monster-stats_">
                                    {{ monster.element }}<span> · </span>
                                    {{ monster.race }}<span> · </span>
                                    {{ monster.size }}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
              </div>
            </div>

             <div v-if="equipment.item_set == 1">
                <div class="clear"></div>
                <div class="sub-heading">
                    <h3>Set effect</h3>
                </div>
                <div class="set-effect">
                  <v-expansion-panels accordion class="accordion" flat="flat">
                    <v-expansion-panel v-for="set in equipment['sets']" :key="set.id">
                      <v-expansion-panel-header>{{ set.equip_suit_desc_en }}</v-expansion-panel-header>
                      <v-expansion-panel-content>
                        {{ set.effect_desc_en }}
                        <div style="display: flex">
                          <div class="col-6" v-for="item in set['items']" :key="item['id']">
                              <div class="item-info">
                                  <div class="image is-24x24">
                                      <img :src="item['icon'] != null ? item['icon'] : '' " :alt="item['name_en'] != null ? item['name_en'] : ''">
                                  </div>
                                  <nuxt-link :to="{ name: 'equipment-slug', params: { slug: item.id }}">
                                      <div class="item-name" @click="openItem(item.id)">
                                          {{ item['name_en'] }}
                                      </div>
                                  </nuxt-link>
                              </div>
                          </div>
                        </div>
                      </v-expansion-panel-content>
                    </v-expansion-panel>

                  </v-expansion-panels>
                </div>
              </div>

            <div  v-if="equipment.type_name == 'Blueprint'">
              <div class="sub-heading clear">
                  <h3>Craft</h3>
              </div>
              <div class="tiers">
                <v-expansion-panels accordion class="accordion" flat="flat">
                  <v-expansion-panel>
                    <v-expansion-panel-header>
                      <div class="attr" style="border: 0; margin-top: 0px;">
                      <dl>
                        <dd class="single-row" style="padding-left: 10px; font-size: 1em;">
                          <div class="image">
                            <img :src="equipment.item_from['icon']" :alt="equipment.item_from['name_en']">
                          </div>
                          {{ equipment.compose[0]['item_output'] }}
                        </dd>
                      </dl>
                      </div>
                      </v-expansion-panel-header>
                    <v-expansion-panel-content>
                      <div class="tier_materials">
                        <dl v-for="material in equipment.compose[0]['materials']" :key="material.id">
                            <dt>
                                <div class="item-info">
                                    <div class="image is-24x24" :class="material['item_id']['type_name'] == 'Blueprint' ? 'blueprint' : ''">
                                        <img :src="material['item_id'] != null ? material['item_id']['icon'] : '' " :alt="material['item_id'] != null ? material['item_id']['name'] : ''">
                                    </div>
                                  <nuxt-link v-if="material['item_id']['type'] == 'items'" :to="{ name: 'item-slug', params: { slug: material['item_id']['slug'] }}" style="line-height: 1.2em; display: flex;">
                                    <div @click="openItem(material['item_id']['slug'])" class="item-name">
                                        {{ material['item_id'] != null ? material['item_id']['name_en'] : '' }} x {{ material['qty'] }}
                                    </div>
                                  </nuxt-link>
                                  
                                  <nuxt-link v-if="material['item_id']['type'] == 'equips'" :to="{ name: 'equipment-slug', params: { slug: material['item_id']['slug'] }}" style="line-height: 1.2em; display: flex;">
                                    <div class="item-name" v-if="material['item_id'] != null && material['item_id']['name_en'] != 'Zeny'">
                                        {{ material['item_id'] != null ? material['item_id']['name_en'] : '' }} x {{ material['qty'] }}
                                    </div>
                                    <div class="item-name" v-else>
                                        {{ material['item_id'] != null ? formatNumber(material['qty']) + ' ' + material['item_id']['name_en'] : '' }}
                                    </div>
                                  </nuxt-link>
                                  <nuxt-link v-if="material['item_id']['type'] == 'cards'" :to="{ name: 'card-slug', params: { slug: material['item_id']['slug'] }}" style="line-height: 1.2em; display: flex;">
                                    <div class="item-name" v-if="material['item_id'] != null && material['item_id']['name_en'] != 'Zeny'">
                                        {{ material['item_id'] != null ? material['item_id']['name_en'] : '' }} x {{ material['qty'] }}
                                    </div>
                                    <div class="item-name" v-else>
                                        {{ material['item_id'] != null ? formatNumber(material['qty']) + ' ' + material['item_id']['name_en'] : '' }}
                                    </div>
                                  </nuxt-link>
                                  
                                  <nuxt-link v-if="material['item_id']['type'] == 'headwears'" :to="{ name: 'headwear-slug', params: { slug: material['item_id']['slug'] }}" style="line-height: 1.2em; display: flex;">
                                    <div class="item-name" v-if="material['item_id'] != null && material['item_id']['name_en'] != 'Zeny'">
                                        {{ material['item_id'] != null ? material['item_id']['name_en'] : '' }} x {{ material['qty'] }}
                                    </div>
                                    <div class="item-name" v-else>
                                        {{ material['item_id'] != null ? formatNumber(material['qty']) + ' ' + material['item_id']['name_en'] : '' }}
                                    </div>
                                  </nuxt-link>
                                </div>
                            </dt>
                        </dl>
                          <dl>
                            <dt>
                                <div class="item-info">
                                    <div class="image is-24x24">
                                        <img src="https://api.ragnarokmobile.net/uploads/items/100_img.png" alt="Zeny">
                                    </div>
                                  <nuxt-link :to="{ name: 'item-slug', params: { slug: 'zeny' }}" style="line-height: 1.2em; display: flex;">
                                    <div @click="openItem('zeny')" class="item-name">
                                        {{ formatNumber(equipment.compose[0]['cost']) }} Zeny
                                    </div>
                                  </nuxt-link>
                                </div>
                            </dt>
                        </dl>
                      </div>
                    </v-expansion-panel-content>
                  </v-expansion-panel>

                </v-expansion-panels>
              </div>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios'
import { constant } from '@/plugins/Constant';

export default {
  name: 'Item',
  components: {
    //
  },

  head() {
    let name_ = this.equipment.name_en;
    let title_ = name_ + ', ' + name_ + ' drop rate, ' + name_ + ' information and attributes, ' + name_ + ' source in Ragnarok Mobile'
    let url_ = 'https://www.ragnarokmobile.net/item/' + this.equipment.slug
    let keywords_ = title_ + ' ROM, ROM Exchange price, market finance, Ragnarok, online, RO, ragnarok mobile, ragnarok m, ragnarok eternal love, database, guide, job, quest, headgear quest, monster drops, item information, skill description, skill simulator, stat calculator, ragnarok tools, ragnarok mobile english'
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
        equipment: {},
        fullPage: false,
    }
  },
  methods: {
    formatNumber(num) {
        if (num != null) return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
    },
    getItem() {
      axios
        .get(constant.getItem+this.id)
        .then(response => (this.equipment = response.data))
        .catch(error => this.$router.replace({name: 'error'}))
        .finally(() => this.loading = false)
    },
    openItem(id) {
      axios
        .get(constant.getItem+id)
        .then(response => (this.equipment = response.data, this.id = this.equipment.id))
        .catch(error => this.$router.replace({name: 'error'}))
        .finally(() => this.loading = false)
    },
  },
  mounted () {
    this.getItem();
  }
}
</script>
<style lang="scss">
.equipment {
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

            &.blueprint {
                background: url('../../assets/images/blueprint.png');
                background-repeat: no-repeat;
                border: 2px solid #c6a460;
            }
            &.fblueprint {
                background-color: #4b8ad5;
                border: 2px solid #4b8ad5;
            }
        }
        img {
           @include imagecontainer_img;
        }
        .item-title {
            text-transform: capitalize;
            font-weight: 500;
            h2 {
                font-size: 1.3em;
                padding: 2px .9em;
                overflow: hidden;
                color: $primary;
                line-height: 20px;
                margin-bottom: 6px;
            }
        }
        .item-title-info {
            margin: -8px 1.2em 3px;
            .type {
                color: $accent;
                font-weight: 600;
                text-transform: uppercase;
                font-size: 0.9em;
                
            }
        }
        .item-tags {
            display: flex;
            margin: 0 1.2em;
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
    .card-type__ {
        margin-left: 6px;
        margin-top: 5px;
        color: $accent;
        font-size: .7em;
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
    .jobs {
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
    }
    .tier_materials {
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
        .image {
            display: inline-block;
            line-height: 10px;
            margin-right: 10px;
            img {
                height: 25px;
                width: 25px;
            }
        }
        .item-name {
            display: flex;
            text-overflow: ellipsis;
            width: 100%;
            font-size: 0.9em;
        }
        
    }
    
    .set-effect {
        .accordion {
            border-radius: 0;
            .v-expansion-panel {
                border: 1px solid $bordercolor;
            }
            .v-expansion-panel-header {
                text-align: left;
                padding: 0px 20px;
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
                font-size: 0.9em;
            }
            .item-info {
                text-align: center;
                align-items: center;
            }
            .image {
                display: inline-block;
                line-height: 10px;
                img {
                    height: 25px;
                    width: 25px;
                }
            }
            .item-name {
                display: flex;
                text-overflow: ellipsis;
                width: 100%;
                font-size: 0.9em;
                place-content: center;
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
        .image {
            display: inline-block;
            line-height: 10px;
            margin-right: 10px;
            img {
                height: 25px;
                width: 25px;
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
            width: 100%;
            padding: 7px 0;
            border-top: 1px solid $bordercolor;
            &:first-child {
                border-top: none;
            }
        }
        dt {
            float: left;
            width: 10em;
            text-indent: 10px;
        }
        dd {
            overflow: hidden;
            color: $secondary;
            &.single-row {
                display: flex;
                align-items: center;
            }
        }
        .full {
            float: none;
            width: auto;
        }
        .single-row {
            font-size: 0.8em;
            .image-container {
                float: left;
                width: 60px;
            }
            .image {
                margin-right: 5px;
                width: 27px !important;
                height: 28px !important;
                @include imagecontainer;
                border: 1px solid #abd2f3;
            }
            img {
                border: 1px solid $white !important;
                width: 25px !important;
                height: 26px !important;
               @include imagecontainer_img;
               padding: 2px;
            }
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

}
</style>
