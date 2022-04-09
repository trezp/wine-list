<template>
  <header><h1>Wine Search</h1></header>
  <ais-instant-search index-name="wine_records" :search-client="searchClient" class="container">
    <aside class="sidebar">
      <h2>Type</h2>
      <ais-refinement-list attribute="type"/>
      <h2>Domain</h2>
      <ais-refinement-list attribute="domain"/> 
      <h2>Year</h2>
      <ais-refinement-list attribute="year"/> 
      <ais-configure :hitsPerPage="6" />
    </aside>
    <main class="search-main">
      <ais-search-box />
      <ais-hits class="wine-results">
        <template v-slot:item="{ item }">
          <div class="wine-details">
            <img :src="item.image" :alt="item.name">
            <h3>{{item.name}}</h3>
            <h4>{{item.domain}}, {{item.year}}</h4>
            <p>${{item.price}}</p>
          </div>
        </template>
      </ais-hits>
    </main>
  </ais-instant-search>
</template>

<script>
import algoliasearch from 'algoliasearch/lite';
import 'instantsearch.css/themes/satellite-min.css';

export default {
  data() {
    return {
      searchClient: algoliasearch(
        'BRNPZODEPO',
        '7a4b8c7ac1f5b076e1c4f82e6caf6764'
      )
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  width: 90%;
  margin: auto;
  display: grid;
  grid-template-areas: 
    "header header header header"
    "aside main main main";
}

.search-main {
  padding: 2em;
}

.sidebar {
  padding: 0 2em;
}

.ais-Hits-list {
  display: flex;
  gap: 10px;
  margin-top: 10px;
  flex-wrap: wrap;

  li {
    flex-basis: calc((100% / 3) - 2em);
    justify-content: center;
  }
}

</style>
