<template>
  <div class="row">
      <div class="col-lg-4 col-md-6 col-sm-6" v-for="lesson in lessons" :key="lesson.id">
          yyy
      </div>
  
    </div>
          
</template>

<script>
export default {
  name: 'Lesson',
  props: ["lessons"]
}
</script>

