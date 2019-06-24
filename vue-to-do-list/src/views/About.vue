<template>
  <div class="about">
    <h1>About</h1>
    <p>This is the about page.</p>
    <p>{{attribute}}</p>
  </div>
</template>


<script>
export default {
  props: ["attribute"]
}
</script>

