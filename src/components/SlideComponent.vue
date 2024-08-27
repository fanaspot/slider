<template>
  <div class="img-container">
    <img :src="imgPath" alt="" />
  </div>
  <div class="slide-info">
    <h1 class="h1">{{ h1 }}</h1>
    <p class="p">
      {{
        p
          ? p
          : "Распродажа мебели и товаров для дома, успей обновить интерьер со скидкой!"
      }}
    </p>
    <button class="btn-info">Подробнее</button>
  </div>
</template>

<script>
export default {
  name: "SlideComponent",
  props: {
    h1: String,
    p: String,
    image: String,
  },
  computed: {
    imgPath() {
      return require(`../assets/img/${this.image}`);
    },
  },
};
</script>
