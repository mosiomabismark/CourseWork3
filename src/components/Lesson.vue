<template>
  <div class="row">
      <div class="col-lg-4 col-md-6 col-sm-6" v-for="lesson in lessons" :key="lesson.id">
        <div class="product__item">
              <div class="product__item__pic set-bg">
                  <img v-bind:src="lesson.image">
                  <ul class="product__item__pic__hover">
                      <li>
                          <button v-on:click="addToCart(lesson)">
                              Add Item To Cart
                              <i class="fa fa-shopping-cart"></i>
                          </button>
                      </li>
                  </ul>
              </div>
          </div>
      </div>
  
    </div>
          
</template>

<script>
export default {
  name: 'Lesson',
  props: ["lessons"],
  methods: {
    addToCart(lesson){
      this.$emit("addItemToCart", lesson);
    }
  }
}
</script>

