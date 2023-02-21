<template>
  <div class="products">
    <div class="container">
      <div class="products-content">
       
          <Products :products="pag" />
        </div>
      </div>
      <div class="products-btns">
        <button @click="prev()">prev</button>
        <div class="products-btns-items">
          <span
            class="btns"
            v-for="(numbs, idx) in pageNumb"
            :key="numbs.idx"
            @click="pages(numbs, idx)"
            >{{ numbs }}</span
          >
        </div>
        <button @click="next()">next</button>
      </div>
    </div>

</template>

<script>
import Products from "./components/ProductsCard.vue";
export default {
  components: { Products },
  data() {
    return {
      products: null,
      pag: null,
      pageNumb: [],
      limit: 200,
      viewNumb: [],
    };
  },
  computed: {},
  methods: {
    async getData() {
      let response = await fetch(
        `https://dummyjson.com/products?limit=${this.limit}`
      );
      let result = await response.json();
      this.products = result.products;
      this.pag = this.products.slice(0, 10);
    },
    pageCount() {
      for (let i = 1; i <= Math.ceil(this.limit / 10); i++) {
        this.pageNumb.push(i);
      }
    },
    pages(numbs) {
      this.pag = this.products.slice(numbs - 1, numbs + 9);
    },
    prev() {
      let x = document.querySelector(".products-btns-items");
      x.scrollLeft -= 100;
    },
    next() {
      let x = document.querySelector(".products-btns-items");
      x.scrollLeft += 100;
    },
  },
  mounted() {
    this.getData();
    this.pageCount();
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial;
}
.container {
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 15px;
}
a {
  text-decoration: none;
}
ul {
  list-style-type: none;
}
.products {
  padding: 100px 0;
  &-btns {
    background: #ccc;
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 5px;
    padding: 10px 20px;
    max-width: 300px;

    &-items {
      overflow-x: scroll;
      overflow-y: hidden;
      &::-webkit-scrollbar {
        height: 0;
      }
    }
    button {
      padding: 15px 20px;
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      &:first-child {
        left: -70px;
      }
      &:last-child {
        right: -70px;
      }
    }
    span {
      cursor: pointer;
      font-size: 20px;
      padding: 5px 10px;
      &:hover {
        font-weight: 700;
      }
    }
    .active {
      color: red;
    }
  }
  &-content {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
    &-items {
      box-shadow: 1px 1px 30px rgba(0, 0, 0, 0.2);
      border-radius: 20px;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: left;
      gap: 15px;
      h2 {
        text-align: center;
        margin: 10px 0;
      }

      img {
        width: 300px;
        text-align: center;
      }
      &-info {
        margin-top: auto;
        display: flex;
        gap: 20px;
        span {
          background: green;
          padding: 10px 15px;
          color: #fff;
        }
      }
    }
  }
}
</style>
