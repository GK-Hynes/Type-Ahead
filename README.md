# Type Ahead

A page created to parse and display an array of US cities. Built for Wes Bos' [JavaScript 30](https://javascript30.com/) course.

[![Screenshot of Type Ahead page](https://screenshots.firefoxusercontent.com/images/5d9f882d-22ab-44dd-9a59-4a2668a84e84.png)](https://gk-hynes.github.io/type-ahead/)

## Notes

This page uses the Fetch API instead of jQuery etc.

Fetch returns a promise, not the data itself. Call `.then` against it and it will return a 'blob' of data.

This 'blob' doesn't know what kind of data it is. Use `blob.json().then()` to return another promise and then get the raw data from it.

To get the data into the empty `cities` array you could set `cities` as a `let` variable.

If you want to keep cities as a `const` variable you can spread the data into it: `cities.push(...data)`.

Call `filter` on the cities array and use a regex to check if the city/state matches the search. (You need this syntax toput a variable into a regular expression.)

```js
function findMatches(wordToMatch, cities) {
  return cities.filter(place => {
    // check if city or state matches what is searched for
    const regex = new RegExp(wordToMatch, "gi");
    return place.city.match(regex) || place.state.match(regex);
  });
}
```

Select the search box and suggestions, listen for a change event/keyup and run the `displayMatches` function.

Use `map` to loop over the returned array and return the html you want to display. (`map` will return an array so you can call `.join('')` on the end to return a string.)

To highlight the search term in the returned city and state names, replace the word with a span with a class of hl and the matched term. Use regexes again here.

```js
const cityName = place.city.replace(
  regex,
  `<span class="hl">${this.value}</span>`
);
```

You can also use regexes to format the population figure which is returned:

```js
function numberWithCommas(x) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
```
