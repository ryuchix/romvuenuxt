<template>
  <div id="bottom-nav">
    <v-bottom-navigation v-if="$route.name != 'index'" fixed grow>
      <nuxt-link to='/' class="v-btn">
        <v-btn aria-label="Home">
          <span>Home</span>
          <img class="icon" src="@/assets/images/icons/home-icon.png" alt="Home"/>
        </v-btn>
      </nuxt-link>

      <nuxt-link to='/monsters' class="v-btn">
        <v-btn aria-label="Monster">
          <span>Monster</span>
          <img class="icon" src="@/assets/images/icons/monster-icon.png" alt="Monster"/>
        </v-btn>
      </nuxt-link>

       <nuxt-link to='/equipments' class="v-btn">
        <v-btn aria-label="Equipment">
          <span>Equipment</span>
          <img class="icon" src="@/assets/images/icons/armor-icon.png" alt="Equipment"/>
        </v-btn>
       </nuxt-link>
       
      <nuxt-link to='/headwears' class="v-btn">
        <v-btn aria-label="Headwear">
          <span>Headwear</span>
          <img class="icon" src="@/assets/images/icons/headwear-icon.png" alt="Headwear"/>
        </v-btn>
      </nuxt-link>
       
      <nuxt-link to='/cards' class="v-btn">
        <v-btn aria-label="Card">
          <span>Card</span>
          <img class="icon" src="@/assets/images/icons/card-icon.png" alt="Card"/>
        </v-btn>
      </nuxt-link>

    </v-bottom-navigation>
  </div>
</template>

<script>
export default {
  name: "Footer",
  components: {
    //
  },
  data() {
    return {
      item: {},
      loading: false,
      offset: true,
      text: "text",
      drawer: false
    };
  },
  methods: {
    //
  }
};
</script>
<style lang="scss">
.v-bottom-navigation {
  background: $white !important;
  a {
    &:last-child {
      @media only screen and (max-width: 768px) {
          display: none;  
      }
    }

  }
}
.v-navigation-drawer {
    left: auto;
    bottom: 0;
    position: fixed !important;
    max-height: 111px !important;
    min-width: 640px !important;

    @media only screen and (max-width: 768px) {
        min-width: 100% !important;  
    }

    .drawer-header {
      background: none !important;
    }

    .section3 {
      display: flex;
    }

    .icons .icon {
        width: 30px;
    }
}

#bottom-nav {
  .more-menu {
    border-radius: 0 !important;
  }

}
  .menuable__content__active {
    border-radius: 0 !important;
    box-shadow: 11px 4px 4px -3px rgba(0, 0, 0, 0.2), 8px 0px 13px 0px rgba(0, 0, 0, 0.14), 7px 4px 10px -2px rgba(0, 0, 0, 0.12) !important;
  
    img {
      width: 25px;
    }
    span {
      font-style: normal;
      font-weight: 300;
      font-weight: 400;
      color: $primary;
      line-height: 1.2;
      font-size: 14px;
      margin-left: 5px;
    }
  }
.v-navigation-drawer {
    left: auto;
    .drawer-header {
        min-height: 50px;
        background: $primary;
        border-bottom: solid 0px rgba(0,0,0,.03);
        box-shadow: 1 4px 18px 0 rgba(0,0,0,.08);
        transition: all 350ms ease;
        .v-list-item__title {
            color: $white;
            font-size: 1rem;
            overflow: hidden;
            white-space: nowrap;
            text-transform: uppercase;
            width: 100%;
            font-weight: bold;
        }
    }
    .subheader {
        text-transform: uppercase;
        font-size: 12px;
        color: #90A4AE;
        font-weight: 400;
        line-height: 24px;
        margin-bottom: -15px;
        line-height: 48px;
        padding-left: 20px;
    }
}

.v-bottom-navigation {
    width: 640px !important;
    max-width: 640px;
    @media only screen and (max-width: 768px) {
        width: 100%;  
        max-width: 100%;
        min-width: 100%;
    }
}

.v-bottom-navigation--fixed {
    margin: 0 auto;
    left: auto !important;
}

.v-bottom-navigation {
    @include userselect;
    button {
        height: inherit !important;
    }
    span {
        @include defaultfont;
        font-weight: 400;
        color: $primary;
    }
    .icon {
        width: 25px;
    }
}
</style>
