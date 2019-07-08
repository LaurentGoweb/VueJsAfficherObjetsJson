<template>
<section class="container-fluid main-container">
  <nav class="navbar navbar-expand">
                 <h1>Traning Vue.js</h1>

              </nav>

    <h2>Page 2</h2>
        <div class="filter">
      <button v-for="(entry, id) in filterList" :item="entry" :key="(entry,id).id" v-on:click="filter = entry; active = id;" :class="{ active: entry == filter }">
        {{ entry }}
      </button>
    </div>
  <div v-for="(entry, id) in users" :item="entry" :key="(entry,id).id">
    <div v-if="resultsFilter(entry, 'fonction', filter)"  class="card">
      <div class="card-body d-flex align-items-center">
        <span class="photo"> <img v-bind:src="entry.photo" /></span>
        <p class="mb-0"><strong>{{ entry.firstName }} {{ entry.lastName }}</strong><br/>{{entry.fonction}}</p>
      </div>
    </div>
  </div>

</section>
</template>

<script>
export default {
   name: "DataDisplay",
    data: function() {
    return {
      fkey: "fonction",
      filterList: ["Front-end", "Back-end", "Commercial", "Tout"],
      filter: "Tout",
      users: []

    };
  },
   created() {
    var apiURL = "https://next.json-generator.com/api/json/get/4JSo_UfEL";
    fetch(apiURL)
      .then(res => res.json())
      .then(res => (this.users = res));
  },
 methods: {
    resultsFilter(entry) {
      if (this.filter !== "Tout") {
        if (entry[this.fkey] === this.filter) {
          return entry;
        }
      } else {
        return entry;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
