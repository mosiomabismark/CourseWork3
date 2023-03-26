<template>
   <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="shoping__cart__table">
                        <table>
                            <thead>
                                <tr>
                                    <th class="shoping__product">Products</th>
                                    <th>Price</th>
                                    <th>Remove</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="lesson in cartItems" :key="lesson.id">
                                    <td class="shoping__cart__item">
                                        <img v-bind:src="lesson.image" alt="">
                                        <h5>{{lesson.subject}}</h5>
                                    </td>
                                    <td class="shoping__cart__price">
                                        ${{lesson.price}}
                                    </td>
                                    <td class="">
                                      <!--
                                        <button v-on:click="deleteCartItem(lesson)">
                                            <span class="icon_close"></span>
                                        </button>
                                      -->
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            
        </div>
</template>

<script>
export default {
  name: 'Checkout',
  props: [
    "cartItems"
  ],
  methods: {
    addToCart(lesson){
      this.$emit("addItemToCart", lesson);
    }
  }
}
</script>

