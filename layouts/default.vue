<template>
  <div id="app" style="margin: 0 auto; background-color: #fafafa">
    <v-app width="640">
      <HeaderBar></HeaderBar>
        <v-fade-transition mode="out-in">
          <keep-alive>
            <nuxt />
          </keep-alive>
      </v-fade-transition>
      <FooterBar></FooterBar>
    </v-app>
  </div>
</template>

<script>
import FooterBar from '@/components/footer.vue';
import HeaderBar from '@/components/header.vue';
export default {
  name: 'DefaultLayout',
  components: {
    FooterBar, HeaderBar
  },
};
</script>

<style lang="scss">
@import '../assets/scss/style.scss';
.v-application--wrap {
  background-color: $white;
  color: $black;
}
.filters span {
    font-size: 0.8em;
    text-transform: uppercase;
    font-weight: 600;
    color: #044F67;
}
</style>
