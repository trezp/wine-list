<template>
  <header>
    <h1>The Wine Club</h1>
  </header>
  <ais-instant-search index-name="wine_records" :search-client="searchClient" class="container">
    <aside class="sidebar">
      <h2>Type</h2>
      <ais-refinement-list attribute="type"/>
      <h2>Price</h2>
      <ais-numeric-menu
        attribute="price"
        :items="[
          { label: 'All' },
          { label: '$10 - $20', start: 10, end: 20 },
          { label: '$20 - $50', start: 20, end: 50 },
          { label: '$50 - $100', start: 50, end: 100 },
          { label: '$100 - $500', start: 100, end: 500 },
          { label: '> $500', start: 500 },
        ]"
      />
      <h2>Region</h2>
      <ais-refinement-list attribute="domain"/> 
      <h2>Year</h2>
      <ais-refinement-list attribute="year"/>
      <ais-configure :hitsPerPage="9" />
    </aside>
    <main>
      <div class="search-and-sort">
        <ais-search-box placeholder="Search wines..." />
        <ais-sort-by id="ais-sort-by"
          :items="[
            { value: 'wine_records', label: 'Highest quality, lowest price' },
            { value: 'wine_asc', label: 'Price low to high' },
            { value: 'wine_desc', label: 'Price high to low' },
          ]"
        />
      </div>
      <ais-infinite-hits class="wine-results">
        <template v-slot:item="{ item }">
          <div class="wine-details">
            <img :src="item.image" :alt="item.name">
            <h3>{{item.name}}, {{item.year}}</h3>
            <h4>{{item.domain}}</h4>
            <p>${{item.price}}</p>
          </div>
        </template>
      </ais-infinite-hits>
      <ais-state-results>
        <template v-slot="{ state: { query }, results: { hits } }">
          <p v-show="!hits.length">No results found. <q>{{ query }}</q></p>
        </template>
      </ais-state-results>
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
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

header {
 margin: 60px 0;
 font-family: 'Poiret One', Helvetica, Arial, sans-serif;
 font-size: 2em;
}

.container {
  max-width: 1920px;
  width: 95%;
  margin: auto;
  display: grid;
  grid-template-areas: 
    "header header header"
    "aside main main";
  grid-template-columns: 25% 75%;
}

.sidebar {
  padding: 0 2em;
  width: 100%;
  text-align: left;
}

h2:first-child {
  margin-top: 0;
}

.search-and-sort {
  display: flex;
  justify-content: space-between;

  .ais-SearchBox {
    width: 70%;
  }
}

.ais-InfiniteHits-list {
  display: flex;
  gap: 10px;
  margin-top: 10px;
  flex-wrap: wrap;

  li {
    flex-basis: calc((100% / 3) - .5em);
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
