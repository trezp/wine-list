<template>
  <header>
    <h1>Find A Wine</h1>
  </header>
  <ais-instant-search index-name="wine_records" :search-client="searchClient" class="container">
    <aside class="sidebar">
      <h2>Type</h2>
      <ais-refinement-list attribute="type"/>
      <h2>Origin</h2>
      <ais-refinement-list attribute="domain"/> 
      <h2>Year</h2>
      <ais-refinement-list attribute="year"/> 
      <ais-configure :hitsPerPage="9" />
    </aside>
    <main>
      <ais-search-box />
      <ais-hits class="wine-results">
        <template v-slot:item="{ item }">
          <div class="wine-details">
            <img :src="item.image" :alt="item.name">
            <h3>{{item.name}}, {{item.year}}</h3>
            <h4>{{item.domain}}</h4>
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
        process.env.VUE_APP_INDEX_ID,
        process.env.VUE_APP_ALGOLIA_API_KEY
      )
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Open Sans',Avenir, Helvetica, Arial, sans-serif;
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
    "header header header header header"
    "aside aside main main main";
}

.sidebar {
  padding: 0 2em;
  width: 100%;
}

.ais-SearchBox {
  width: 95%;
}

.ais-Hits-list {
  display: flex;
  gap: 10px;
  margin-top: 10px;
  flex-wrap: wrap;

  li {
    flex-basis: calc((100% / 3) - 2em);
    justify-content: center;

    &:hover {
      box-shadow: 0 0 0 1px rgb(35 38 59 /20%), 0 1px 3px 0 rgb(35 38 59 / 70%);
    }
  }

  h4 {
    font-style: italic;
  }

  p {
    font-weight: bold;
    font-size: 1.2em;
  }
}

</style>
