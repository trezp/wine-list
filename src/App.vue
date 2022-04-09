<template>
  <h1>Wine Sherpa</h1>
  <ais-instant-search index-name="wine_records" :search-client="searchClient">
    <h2>Type</h2>
    <ais-refinement-list attribute="type"/>
    <h2>Domain</h2>
    <ais-refinement-list attribute="domain"/> 
    <h2>Year</h2>
    <ais-refinement-list attribute="year"/> 
    <ais-search-box />
    <ais-configure :hitsPerPage="5" />
    <ais-hits>
      <template v-slot:item="{ item }">
        <h3>{{item.name}}</h3>
        <h4>{{item.domain}}</h4>
        <p>{{item.year}}</p>
        <img :src="item.image" :alt="item.name">
        <p>${{item.price}}</p>
      </template>
    </ais-hits>
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

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
