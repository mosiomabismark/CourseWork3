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
                                        <button v-on:click="deleteCartItem(lesson)">
                                            <span class="icon_close"></span>
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            
            <div class="row">
                <div class="col-lg-12">
                </div>
                <div class="col-lg-6">
                    <div class="shoping__continue">
                        <div class="shoping__discount">
                            <h5>Billing Details</h5>
                            <form action="#">
                                <div class="alert alert-light text-danger" role="alert">
                                    {{ errors.first("fullName") || errors.first("phoneNumber") }}
                                </div>
                                <div class="row">
                                    <div class="col-lg-6">
                                        <div class="checkout__input">
                                            <p>Full Name<span>*</span></p>
                                            <input type="text" name="fullName" :value="fullName" @input="$emit('update:fullName', $event.target.value)" v-validate="'required|alpha_spaces'" required>
                                        </div>
                                    </div>
                                    <div class="col-lg-6">
                                        <div class="checkout__input">
                                            <p>Phone<span>*</span></p>
                                            <input type="text" name="phoneNumber" :value="phoneNumber" @input="$emit('update:phoneNumber', $event.target.value)" v-validate="'required|numeric'" required>
                                        </div>
                                    </div>
                                </div>
                              <!--
                                <button class="primary-btn w-100" v-bind:disabled="!checkoutErrorsExist(errors.first('fullName'), errors.first('phoneNumber'))" v-on:click="submitCheckout">PROCEED TO CHECKOUT</button>
                              -->
                              </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
export default {
  name: 'Checkout',
  props: [
    "cartItems",
    "fullName",
    "phoneNumber"
  ],
  methods: {
    deleteCartItem(lesson){
      this.$emit("deleteCartItem", lesson);
    }
  }
}
</script>

