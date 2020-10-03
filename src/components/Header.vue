<template>
  <header class="header">
    <div class="header__top">
      <div class="container header__container">
        <a href="#" class="location">
          <span class="location__icon"></span>
          <span>Волгоградская область</span>
        </a>
        <div class="menu">
          <div class="menu__item">
            <a class="menu__link" href="/">Тендеры</a>
          </div>
          <div class="menu__item">
            <a class="menu__link" href="/">База подрядчиков</a>
          </div>
          <div class="menu__item">
            <a class="menu__link" href="/">
              <span>Другие сервисы</span>
              <span class="menu__icon"></span>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="header__bottom">
      <div class="container header__container">
        <div class="header__logo">
          <a href>
            <img src="../assets/images/logo.png" alt />
          </a>
        </div>
        <div class="catalog">
          <a class="catalog__button" href>
            <div class="catalog__icon">
              <span></span>
              <span></span>
              <span></span>
            </div>
            <span>Каталог</span>
          </a>
        </div>
        <div class="search">
          <form class="search__form">
            <input
              v-model="search"
              @focus="searchResult=true"
              class="search__input"
              autocomplete="off"
              type="text"
              placeholder="Хочу найти..."
            />
            <span ref="searchIcon" class="search__icon"></span>
          </form>
          <div class="search__result" v-if="result && searchResult">
            <div
              class="search__item"
              v-for="(resultItem, index) in result"
              :key="index"
              @click="setResult(resultItem)"
            >{{resultItem}}</div>
          </div>
        </div>
        <div class="list">
          <div class="list__button">
            <div class="list__icon">
              <span class="list__icon-img"></span>
              <span class="list__icon-indicator"></span>
            </div>
            <span class="list__header">Список</span>
          </div>
        </div>
        <div class="account">
          <div class="account__avatar">
            <img src="../assets/images/ava.png" alt />
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      search: "",
      catalog: ["Двери", "Лестницы", "Окна", "Асфальт"],
      result: [],
      searchResult: false
    };
  },
  mounted() {
    this.searchCatalog();
  },
  methods: {
    searchCatalog() {
      if (this.search.length == 0) {
        this.result = this.catalog;
      } else {
        this.$refs.searchIcon.style.display = "none";
      }
      this.result = this.catalog.filter(item =>
        item.toLowerCase().startsWith(this.search.toLowerCase())
      );
      // this.result = this.catalog.filter(item =>
      //   item.toLowerCase().includes(this.search.toLowerCase())
      // );
    },
    setResult(item) {
      this.search = item;
      this.searchResult = false;
    }
  },
  watch: {
    search() {
      this.searchCatalog();
    }
  }
};
</script>

<style scoped lang="scss">
.header {
  &__container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }
  &__top {
    position: relative;
    background-color: #fafbfc;
    border-bottom: 1px solid #eceff1;
  }
  &__bottom {
    position: relative;
    padding: 14px 0;
    border-bottom: 1px solid #eceff1;
  }
}

.location {
  display: flex;
  align-items: center;
  font-size: 12px;
  color: #708598;
  text-decoration: none;

  &__icon {
    display: block;
    min-width: 14px;
    height: 16px;
    background-image: url("../assets/images/location.svg");
    margin-right: 8px;
  }
}

.menu {
  display: flex;
  align-items: center;
  min-height: 32px;

  &__item {
    padding: 0 22px;

    &:last-child {
      padding-right: 0;
    }
  }

  &__link {
    color: #708598;
    font-size: 12px;
    text-decoration: none;
    display: flex;
    align-items: center;
  }

  &__icon {
    display: block;
    min-width: 18px;
    height: 18px;
    background-image: url("../assets/images/dropdown.svg");
    margin-left: 2px;
  }
}

.catalog {
  &__button {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #fed83d;
    color: #000;
    border-radius: 4px;
    text-decoration: none;
    width: 116px;
    height: 40px;
  }
  &__icon {
    display: block;
    width: 17px;
    margin-right: 10px;
    span {
      display: block;
      background-color: #000;
      width: 100%;
      height: 2px;

      &:nth-child(2) {
        margin-top: 2px;
      }
      &:nth-child(3) {
        margin-top: 2px;
      }
    }
  }
}

.search {
  position: relative;

  &__input {
    width: 498px;
    height: 40px;
    padding: 0 14px;
    border: 1px solid #eceff1;
    border-radius: 4px;
  }

  &__icon {
    position: absolute;
    background-image: url("../assets/images/search.svg");
    width: 20px;
    height: 20px;
    right: 14px;
    top: 10px;
    bottom: 0;
  }
  &__result {
    position: absolute;
    left: 0;
    right: 0;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.03);
    z-index: 3;
    background-color: #fff;
  }
  &__item {
    padding: 12px;
    cursor: pointer;

    &:hover {
      background-color: #eceff1;
    }
  }
}

.list {
  &__button {
    width: 111px;
    height: 40px;
    background-color: #fafbfc;
    border: 1px solid #eceff1;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  &__icon {
    position: relative;
    &-img {
      display: block;
      background-image: url("../assets/images/list.svg");
      min-width: 18px;
      height: 22px;
      margin-right: 9px;
    }

    &-indicator {
      position: absolute;
      top: -3px;
      right: 5px;
      display: block;
      width: 10px;
      height: 10px;
      background-color: #e92f2f;
      border: 2px solid #fafbfc;
      border-radius: 90%;
      box-sizing: border-box;
    }
  }

  &__header {
    font-weight: 600;
    font-size: 14px;
    color: #050f19;
  }
}
</style>
