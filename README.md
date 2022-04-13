# The Wine Club

Welcome to the Wine Club! My goal was to create an experience to serve both wine connoisseurs who know what they're looking for and novices who may need help finding the highest quality wine at their price point. This demo seeks to anticipate what is most important to the wine buyer: What's the best wine I can get in my price range? What type of wine is it? Where is it from? What year is its vintage? 

This search experience offers the following features: 

- Users can search wines by what's most relevant to wine buyers: name, domain/region, type, and year 
- User can filter results by a variety of price ranges, in addition to type, region, and year 
- By default, wines are custom ranked by quality and price (highest quality at lowest price)
- Additionally, two dataset replicas allow the user to sort by price low to high, or price high to low 
- Choosing a wine can be overwhelming. Infinite results display nine wines by default, but user can opt to look at more

If I had more time to work with this demo, I would have liked to do the following: 
- Personalize the styling of the demo a little more. As that would largely depend upon the client's branding, I focused on building a clean, simple and intuitive interface, placing the search bar and filters where they tend to be placed in other retail search/sort/filter experiences (eg Best Buy, Amazon), with the filtering options as a left sidebar and search/sort along the top 
- Add the ability to sort by featured wines, to help narrow the inventory for curious buyers  
- Further CSS tweaks to ensure that the demo is fully responsive  

## Project setup
```
npm install
```

### Create a .env file with the `wine_records` index id and api key: 
```
VUE_APP_INDEX_ID=XXXX
VUE_APP_ALGOLIA_API_KEY=XXXX
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
