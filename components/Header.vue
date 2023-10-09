<template>
  <header id="header" class="header" :class="{scrolled: scrl}">
    <div class="content flex justify-between">
      <div class="header__logo">
        <nuxt-link :to="`/${lang}`" class="header__logo-link">
          <img :src="this.$config.axios.logo ? this.$config.axios.logo : '/img/shogun_text_logo.png'" class="logo-desc" alt="logo" />
          <img :src="this.$config.axios.logo ? this.$config.axios.logo : '/img/shogun_text_logo.png'" class="logo-mob" alt="logo" />
        </nuxt-link>
      </div>
      <div class="header__etc flex justify-between flex-no-wrap">
        <div class="header__language" @click.stop="toggleLangMenu">
          <div class="header__language-current">
            <span>
              {{lang}}
            </span>
            <img class="header__language-arr" src="/img/arr.svg" />
          </div>
          <ul :class="['navigation-language', { active: isMenuActivated.lang }]">
            <li class="navigation-language__item" v-for="item in ['en', 'ru']" :key="item">
              <a
                :class="[
                  'navigation-language__link',
                  { selected: lang === item },
                ]"
                @click.prevent="setLang(item)"
              >{{ item }}</a
              >
            </li>
          </ul>
        </div>
        
        <a href="https://shogunapp.movement-defi.xyz/" class="header-btn">{{ $t('Launch App') }}</a>
        
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      isMenuActivated: {
        lang: false,
        page: false
      },
      scrl: false
    }
  },
  computed: {
    lang() {
      return this.$store.getters.lang
    },
  },
  methods: {
    closeAll(){
      this.isMenuActivated.lang = false
      this.isMenuActivated.page = false
    } ,
    toggleLangMenu() {
      this.isMenuActivated.lang = !this.isMenuActivated.lang
      this.isMenuActivated.page = false
    },
    togglePageMenu() {
      this.isMenuActivated.page = !this.isMenuActivated.page
      this.isMenuActivated.lang = false
    },
    setLang(lang) {
      if (this.$route.params.lang !== lang) {
        this.$store.commit('SET_LANG', lang)
        const toLang = this.$route.params.lang
        const path = this.$nuxt.$route.path.replace(toLang, lang)
        this.$i18n.setLocale(lang)
        localStorage.setItem('lang', lang)
        this.$router.push({path: path})
      }
    },

    removeHandlers() {
      document.body.removeEventListener('click', this.closeAll)
    },

    addHandlers() {
      document.body.addEventListener('click', this.closeAll)
    },

    scrollAction() {
      const onScroll = () => {
        const scroll = document.documentElement.scrollTop
        if (scroll > 0) {
          this.scrl = true
        } else {
          this.scrl = false
        }
      }
      window.addEventListener('scroll', onScroll)
    }
  },

  beforeDestroy() {
    this.removeHandlers()
  },

  mounted() {
    this.addHandlers()
    this.scrollAction()
  },
}
</script>

<style scoped lang='scss'>
.header {
  padding-top: 37px;
  height: 150px;
  position: absolute;
  top: 0;
  width: 100%;
  z-index: 2;
}
.header__etc {
  padding-top: 6px;
}

.header-btn {
  width: 200px;
  height: 46px;
  border: 1px solid #483D89;
  border-radius: 5px;
  text-align: center;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 52px;
}
.header-btn:hover {
  color: #bbbbbb;
}
.header__language {
  position: relative;
  display: none !important;
}
.header__language-current {
  width: 102px;
  height: 46px;
  border: 1px solid #483D89;
  border-radius: 5px;
  text-align: center;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
}

.header__language-current span {
  text-transform: uppercase;
}
.logo-mob {
  display: none;
}
.logo-desc {
  display: inline-block;
}
@media (max-width: 900px) {
  .header {
    height: 40px;
  }
  .logo-mob {
    display: inline-block;
  }
  .logo-desc {
    display: none;
  }
  .header {
    background: transparent;
    padding-top: 15px;
  }
  .header__logo {
    width: 100px;
  }
  .header__language-current {
    color: #000;
    height: 42px;
    border-radius: 0;
    position: relative;
    top: -1px;
    width: 70px;
  }
  .header-btn {
    color: white;
    padding: 5px 2px;
    border: 1px solid gray;
    position: relative;
    top: 5px;
    width: 120px;
    height: 35px
  }
  .burger {
    width: 40px;
    height: 40px;
    border-radius: 0;
    margin-right: -20px;
    margin-left: 0;
  }
  .navigation.navigation__open {
    position: absolute;
    top: 46px;
    right: -14px;
    display: block;
    width: 223px;
  }
  .header__etc {
    padding-top: 0;
    margin-top: -8px;
  }
  .burger__text {
    display: none;
  }
}
</style>
