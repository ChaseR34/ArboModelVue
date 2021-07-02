<template>
<div class="tutorial">
  <section class="section">
    <div class="column is-4">
      <div class="card">
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4"> {{ name }}</p>
            </div>
          </div>
          <div class="content" v-if="showDescription">
            <p>{{ description}}</p>
          </div>
          <div class="content">
            <p>"Missing Description"</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</div>

</template>

<script>
export default {
  name: "TutorialVue",
  data (){
    return {
      name: "Vue Hero",
      description: "I'm the description",
      showDescription: false
    }

  }
}
</script>

<style scoped>

</style>