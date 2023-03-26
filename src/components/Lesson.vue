<template>
  <div class="row">
      <div class="col-lg-4 col-md-6 col-sm-6" v-for="lesson in lessons" :key="lesson.id">
        <div class="product__item">
              <div class="product__item__pic set-bg">
                  <img v-bind:src="lesson.image">
                  <ul class="product__item__pic__hover">
                      <li>
                          <button v-on:click="addToCart(lesson)" v-if="canAddToCart(lesson)">
                              Add Item To Cart
                              <i class="fa fa-shopping-cart"></i>
                          </button>
                      </li>
                  </ul>
              </div>
              <div class="product__item__text">
                  <h6>{{lesson.subject}}</h6>
                  <h6>{{lesson.location}}</h6>
                  <h6>${{lesson.price}}</h6>
                  <h6>{{lesson.stock - cartCount(lesson.subjectId)}} left</h6>
              </div>
          </div>
      </div>
  
    </div>
          
</template>

<script>
export default {
  name: 'Lesson',
  props: [
    "lessons",
    "canAddToCart",
    "cartCount"
  ],
  methods: {
    addToCart(lesson){
      this.$emit("addItemToCart", lesson);
    }
  }
}
</script>

