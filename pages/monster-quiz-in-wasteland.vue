<template>
<div id="app">
  <v-app>
  <div class="content">

    <h2>Monster Quiz in Wasteland</h2>
    <p>One of the new daily instances in Wasteland map is Monster quiz. Monsters will spawn in the field and you need to count the monsters in the area based from the given question. So here's the cheatsheet that will help you in the game.</p>
    <v-tabs v-model="tab" background-color="indigo" color="white" grow centered show-arrows next-icon prev-icon>
      <v-tab>Legs</v-tab>
      <v-tab>Race</v-tab>
      <v-tab>Element</v-tab>
      <v-tab>Color</v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-card
          color="white"
          flat>
          <v-card-text>
            <h3>Apodous (0 leg)</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100990_img.png" alt="Marin">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100010_img.png" alt="Poring">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200170_img.png" alt="Mastering">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100250_img.png" alt="Marina">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100030_img.png" alt="Fabre">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/40009_img.png" alt="PUpa">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101910_img.png" alt="man Eating grass">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200020_img.png" alt="Eclipse">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100020_img.png" alt="Lunatic">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200230_img.png" alt="Rafflesia">
            <br>
            <h3>Biped (2 legs)</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100130_img.png" alt="Willow">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100550_img.png" alt="Bigfoot">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100450_img.png" alt="Giearth">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/300130_img.png" alt="Moonlight flower">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200030_img.png" alt="Vocal">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101550_img.png" alt="Harpy">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101250_img.png" alt="Mantis">
            <br>
            <h3>Quadruped (4 legs)</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100670_img.png" alt="Ninetails">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101390_img.png" alt="Desert baby wolf">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100160_img.png" alt="Wolf">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/181630_img.png" alt="stem worm">
          </v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card
          color="white"
          flat>
          <v-card-text>
            <h3>Insect</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/40009_img.png" alt="PUpa">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200030_img.png" alt="Vocal">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101250_img.png" alt="Mantis">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100030_img.png" alt="Fabre">
            <br>
            <h3>Brute/Animal</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101390_img.png" alt="Desert baby wolf">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100160_img.png" alt="Wolf">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100550_img.png" alt="Bigfoot">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200020_img.png" alt="Eclipse">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100020_img.png" alt="Lunatic">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100670_img.png" alt="Ninetails">
            <br>
            <h3>Plant</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100990_img.png" alt="Marin">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100010_img.png" alt="Poring">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200170_img.png" alt="Mastering">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100250_img.png" alt="Marina">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100130_img.png" alt="Willow">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/181630_img.png" alt="stem worm">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101910_img.png" alt="man Eating grass">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200230_img.png" alt="Rafflesia">
            <br>
            <h3>Demon</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100450_img.png" alt="Giearth">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101550_img.png" alt="Harpy">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/300130_img.png" alt="Moonlight flower">
          </v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card
          color="white"
          flat>
          <v-card-text>
            <h3>Fire</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/300130_img.png" alt="Moonlight flower">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100670_img.png" alt="Ninetails">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200030_img.png" alt="Vocal">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101390_img.png" alt="Desert baby wolf">
            <br>
            <h3>Wind</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101550_img.png" alt="Harpy">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/181630_img.png" alt="stem worm">
            <br>
            <h3>Neutral</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200020_img.png" alt="Eclipse">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100020_img.png" alt="Lunatic">
            <br>
            <h3>Earth</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100130_img.png" alt="Willow">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100450_img.png" alt="Giearth">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/40009_img.png" alt="PUpa">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100550_img.png" alt="Bigfoot">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200230_img.png" alt="Rafflesia">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101910_img.png" alt="man Eating grass">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101250_img.png" alt="Mantis">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100030_img.png" alt="Fabre">  
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100160_img.png" alt="Wolf">
            <br>
            <h3>Water</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100990_img.png" alt="Marin">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100010_img.png" alt="Poring">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200170_img.png" alt="Mastering">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100250_img.png" alt="Marina">
          </v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card
          color="white"
          flat>
          <v-card-text>
            <h3>Yellow</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101550_img.png" alt="Harpy">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/300130_img.png" alt="Moonlight flower">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200030_img.png" alt="Vocal">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100670_img.png" alt="Ninetails">
            <br>
            <h3>Red</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100010_img.png" alt="Poring">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200170_img.png" alt="Mastering">
            <br>
            <h3>Brown</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101390_img.png" alt="Desert baby wolf">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100130_img.png" alt="Willow">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100550_img.png" alt="Bigfoot">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100450_img.png" alt="Giearth">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/40009_img.png" alt="PUpa">
            <br>
            <h3>Blue</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100990_img.png" alt="Marin">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200020_img.png" alt="Eclipse">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100160_img.png" alt="Wolf">
            <br>
            <h3>White</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/181630_img.png" alt="stem worm">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100990_img.png" alt="Marin">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100020_img.png" alt="Lunatic">
            <br>
            <h3>Green</h3>
            <img src="https://api.ragnarokmobile.net/uploads/monsters/100030_img.png" alt="Fabre">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101910_img.png" alt="man Eating grass">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/200230_img.png" alt="Rafflesia">
            <img src="https://api.ragnarokmobile.net/uploads/monsters/101250_img.png" alt="Mantis">
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
    <h2>Tips</h2>
    <p>Release your pet and cat mercenaries to avoid overlapping with other monsters on the field.</p>
    <p>If the questions includes <strong>AND</strong> / <strong>OR</strong>, just keep in mind that <strong>OR</strong> only requires either A or B as answer. For <strong>AND</strong>, it means you need to satisfy both A and B to answer it correctly.</p>
  </div>
  </v-app>
  </div>
</template>
<script>
export default {
  head() {
    let title_ = "Monster quiz in Wasteland | Ragnarok Mobile - Guide, Quest, Build and Database for Ragnarok M Eternal Love"
    let url_ = 'https://www.ragnarokmobile.net/monster-quiz-in-wasteland'
    let keywords_ = 'monster quiz, monster photography, wasteland map, wasteland tree, hourglass, hour glass, quiz cheat, monster quiz guide'
    let description_ = 'One of the new daily instances in Wasteland map is Monster quiz. Monsters will spawn in the field and you need to count the monsters in the area based from the given question. So heres the cheatsheet that will help you in the game.'
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
          content: 'https://www.ragnarokmobile.net/img/monsterquiz.png'
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
      tab: null,
    }
  }
}
</script>