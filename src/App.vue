<template>
  <div id="app">
         <!-- Header Section Begin -->
    <header class="header">
        <div class="container">
            <div class="row">
                <div class="col-lg-3">
                    <h3>{{sitename}}</h3>
                </div>
                <div class="col-lg-6">
                </div>
                <div class="col-lg-3">
                    <div class="header__cart">
                        <button v-bind:disabled="cartItemCount===0" v-on:click="showCheckout"><i class="fa fa-shopping-bag"></i> <span>{{cartItemCount}}</span></button>
                    </div>
                </div>
            </div>

        </div>
    </header>
    <!-- Header Section End -->

    <!-- Hero Section Begin -->
    <section class="hero hero-normal">
        <div class="container">
            <div class="row">
                <div class="col-lg-3">
                </div>
                <div class="col-lg-9">
                    <div class="hero__search">
                        <div class="hero__search__form">
                            <form action="#">
                                <input type="text" placeholder="What do yo u need?" v-model="searchItem">
                                <button type="submit" class="site-btn">SEARCH</button>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Hero Section End -->
    <!-- Product Section Begin -->



    <section class="product spad" v-if="showLesson">
        <div class="container">
            <div class="row">
                <div class="col-lg-3 col-md-5">
                    <div class="sidebar">
                        <div class="sidebar__item">
                            <h4>Filter By</h4>
                            <input type="radio" id="ascending" name="ascending" value="ascending" v-model="filterItem">
                            <label for="ascending"> Ascending</label><br>
                            <input type="radio" id="descending" name="descending" value="descending" v-model="filterItem">
                            <label for="descending">Descending</label><br>
                        </div>
                    </div>
                </div>
                <div class="col-lg-9 col-md-7">
                    <div class="filter__item">
                        <div class="row">
                            <div class="col-lg-4 col-md-5">
                                <div class="filter__sort">
                                    <span>Sort By</span>
                                    <select v-model="sortItem">
                                        <option value="subject">Subject</option>
                                        <option value="price">Price</option>
                                        <option value="location">Location</option>
                                        <option value="stock">Stock</option>
                                    </select>
                                </div>
                            </div>
                            <div class="col-lg-4 col-md-4">
                            </div>
                            <div class="col-lg-4 col-md-3">
                            </div>
                        </div>
                    </div>

                    <Lesson 
                      :lessons="(!searchedItems.length ? sortLessons : searchedItems)" 
                      @addItemToCart="addToCart"
                      :canAddToCart="canAddToCart"
                      :cartCount="cartCount"
                    />
                     
                </div>
            </div>
        </div>
    </section>
    <!-- Product Section End -->   
    
    <!-- Shoping Cart Section Begin -->
    <section class="shoping-cart spad" v-else>

        <Checkout
          :cartItems="cartItems"
          @deleteCartItem="deleteCartItem"
          :fullName.sync="fullName"
          :phoneNumber.sync="phoneNumber"
          :checkoutErrorsExist="checkoutErrorsExist"
          @submitCheckout="submitCheckout"
        />

    </section>
    <!-- Shoping Cart Section End -->

    </div>
</template>

<script>
import Lesson from './components/Lesson.vue'
import Checkout from './components/Checkout.vue'


export default {
  name: 'App',
  components: {
    Lesson,
    Checkout
  },
  data(){
    return {
      sitename: "CW-CST3145",
      lessons: lessons,
      cart:[],
      sortItem: "",
      filterItem: "ascending",
      showLesson: true,
      cartItems: [],
      fullName: "",
      phoneNumber: "", 
      searchItem: ""
    }
  },
  methods: {
      addToCart(lesson){
          this.cart.push(lesson.subjectId);
          this.cartItems.push(lesson);
      },
      canAddToCart(lesson) {
          return lesson.stock > this.cartCount(lesson.subjectId);
      },
      cartCount(subjectId) {
          let count = 0;
          for (let i = 0; i < this.cart.length; i++) {
              if (this.cart[i] === subjectId) {
                  count++;
              }
          }
          return count;
      },
      showCheckout() {
          this.showLesson = this.showLesson ? false : true;
      },

      deleteCartItem(lesson){
          var index = this.cart.indexOf(lesson.subjectId);
          if (index !== -1) {
              this.cart.splice(index, 1);
              this.cartItems.splice(index, 1);
          }
      },
      checkoutErrorsExist(fullNameErrors, phoneNumberErrors){
          let errorsExist;
          if((fullNameErrors === undefined || phoneNumberErrors === undefined) && (this.fullName === "" || this.phoneNumber === "")){
              errorsExist = false;
          } else {
              errorsExist = !fullNameErrors && !phoneNumberErrors;
          }
          return errorsExist;
      },
      submitCheckout(){
          alert("Order has been submitted.");
      }

  },
  computed: {
      cartItemCount() {
          return this.cart.length;
      },
      sortLessons(){
          let lessonsArr = this.lessons.slice(0);
          const compare = (a, b) => {
              if (a[this.sortItem] > b[this.sortItem])
                  return 1;
              if (a[this.sortItem] < b[this.sortItem])
                  return -1;
              return 0;
          };
          if (this.filterItem === "descending") {
              lessonsArr.sort(compare);
              return lessonsArr.reverse();
          } else {
              return lessonsArr.sort(compare);
          }
      },
      searchedItems(){
          let searchedSubjectsArr = [];
          if(this.searchItem !== ""){
              for(let i = 0;  i < this.lessons.length; i++){
                  let upperCaseSearchTerm = this.searchItem.toUpperCase();
                  let upperCaseSubjectTitle = this.lessons[i].subject.toUpperCase();
                  let upperCaseSubjectLocation = this.lessons[i].location.toUpperCase();
                  if(upperCaseSubjectTitle.includes(upperCaseSearchTerm) || upperCaseSubjectLocation.includes(upperCaseSearchTerm)){
                      searchedSubjectsArr.push(this.lessons[i])
                  }
              }
          }
          return searchedSubjectsArr;
      }
  }
}
</script>
