<template>
  <header class="header">
    <container class="header__container">
      <div class="header__title-wrapper">
        <nuxt-link to="/" class="header__link">
          <h3 class="header__title">{{ headerData.title }}</h3>
        </nuxt-link>
        <button
          :class="`header__hider header__hider_${isMenuActive()}`"
          @click="menuToggle"
        ></button>
      </div>
      <div :class="`header__wrapper header__wrapper_${isMenuActive()}`">
        <main-menu class="header__menu" />
        <main-button
          class="header__share-story"
          color="purple"
          type="button"
          :disabled="false"
          @buttonClick="QuestionnaireOpen"
          :header="true"
        >
          Рассказать историю
        </main-button>
      </div>
    </container>
  </header>
</template>

<script>
import Menu from '@/components/ui/Menu';
import Container from '@/components/ui/Container';
import Button from '@/components/ui/Button';
export default {
  components: {
    'main-menu': Menu,
    container: Container,
    'main-button': Button,
  },
  methods: {
    QuestionnaireOpen() {
      this.$store.commit('questionnaire/openQuestionnaire');
    },
    menuToggle() {
      this.$store.commit('header-menu/toggleMobileMenu');
    },
    isMenuActive() {
      return this.isMobileMenuOpened ? 'active' : 'inactive';
    },
  },
  computed: {
    isMobileMenuOpened() {
      return this.$store.getters['header-menu/getMobileMenuState'];
    },
    headerData() {
      return this.$store.getters['blocks/getHeaderBlock'];
    },
  },
};
</script>

<style scoped>
.header {
  padding: 18px 0;
  margin: 0;
  border-bottom: 1px solid #e8e8e8;
  display: flex;
}

.header__container {
  display: flex;
  justify-content: space-between;
}

.header__hider {
  display: none;
}
.header__title {
  font-weight: 600;
  font-size: 16px;
  line-height: 20px;
  margin: 0;
  max-width: 340px;
}

.header__link {
  color: #000;
  text-decoration: none;
}

.header__wrapper {
  display: flex;
  margin: 9px 13px 0 0;
}

.header__share-story {
  width: 218px;
  height: 44px;
  margin: -8px 0 0 40px;
  transition: all linear 0.3s;
  line-height: 20px;
  font-size: 16px;
  line-height: 24px;
}

.header__share-story:hover {
  background-color: #fff;
  color: #613a93;
  border: 1px solid #613a93;
}

@media screen and (max-width: 1280px) {
  .header__title {
    line-height: 18px;
  }
  .header__wrapper {
    margin: 6px 11px 0 0;
  }
  .header__share-story {
    margin: -5px 0 0 42px;
    width: 211px;
    height: 42px;
  }
}
@media screen and (max-width: 1024px) {
  .header__share-story {
    width: 201px;
    height: 38px;
    font-size: 15px;
    line-height: 18px;
  }
}

@media screen and (max-width: 835px) {
  .header__container {
    flex-direction: column-reverse;
    position: relative;
  }

  .header__wrapper {
    margin: 0 11px 18px 0;
    border-bottom: 1px solid #efefef;
    padding: 0 0 18px;
  }

  .header__wrapper_active {
    display: flex;
  }

  .header__wrapper_inactive {
    display: none;
  }

  .header__share-story {
    margin: 0 0 0 32px;
    width: 200px;
    height: 38px;
  }

  .header__title-wrapper {
    display: flex;
    justify-content: space-between;
  }

  .header__hider {
    margin: 4.5px 1px 0 0;
    padding: 0;
    height: 27px;
    width: 32px;
    display: block;
    background-image: url('/images/hider.svg');
    background-position: center;
    background-size: contain;
    background-repeat: no-repeat;
    border: none;
    background-color: #fff;
    outline: none;
  }

  .header__hider_active {
    background-image: url('/images/hider-open.svg');
    margin: 4.5px 0 0;
  }
}

@media screen and (max-width: 480px) {
  .header {
    padding: 18px 0 17px;
  }

  .header__hider {
    margin: 0;
  }

  .header__title {
    font-size: 12px;
    line-height: 14px;
  }
  .header__wrapper {
    flex-direction: column;
    margin: 0 11px 17px 0;
    align-items: flex-start;
  }
  .header__menu /deep/ .menu {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .header__menu /deep/ .menu__navigation-el {
    font-size: 13px;
    line-height: 16px;
    margin: 0;
  }

  .header__menu /deep/ .menu__navigation-el:last-child {
    margin-top: 18px;
  }
  .header__share-story {
    margin: 18px 0 0;
    font-size: 12px;
    line-height: 15px;
    width: 146px;
    height: 31px;
  }
}
</style>
