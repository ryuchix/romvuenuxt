<template>
  <div>
    <Neutral v-if="element == 'Neutral'"></Neutral>
    <Fire v-if="element == 'Fire'"></Fire>
    <Water v-else-if="element == 'Water'"></Water>
    <Wind v-else-if="element == 'Wind'"></Wind>
    <Earth v-else-if="element == 'Earth'"></Earth>
    <Holy v-else-if="element == 'Holy'"></Holy>
    <Dark v-else-if="element == 'Shadow'"></Dark>
    <Ghost v-else-if="element == 'Ghost'"></Ghost>
    <Undead v-else-if="element == 'Undead'"></Undead>
    <Poison v-else-if="element == 'Poison'"></Poison>
  </div>
</template>
<script>
import Neutral from '@/components/Elements/Neutral.vue';
import Fire from '@/components/Elements/Fire.vue';
import Water from '@/components/Elements/Water.vue';
import Wind from '@/components/Elements/Wind.vue';
import Earth from '@/components/Elements/Earth.vue';
import Holy from '@/components/Elements/Holy.vue';
import Dark from '@/components/Elements/Dark.vue';
import Ghost from '@/components/Elements/Ghost.vue';
import Undead from '@/components/Elements/Undead.vue';
import Poison from '@/components/Elements/Poison.vue';

export default {
  name: 'Elemental',
  props: [
    'element'
  ],
  components: {
    Neutral, Fire, Water, Wind, Earth, Holy, Dark, Ghost, Undead, Poison
  }
}
</script>
<style lang="scss">
.tddehighlight {
  background-image: linear-gradient(-100deg, rgba(255, 255, 255, 0), #ccc 85%, rgba(255, 255, 255, 0));
  width: fit-content;
}
.tdhighlight {
  background-image: linear-gradient(-100deg, rgba(255, 255, 255, 0), #caf371 85%, rgba(255, 255, 255, 0));
  width: fit-content;
}
</style>