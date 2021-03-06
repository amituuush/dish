# Dish Application

## What does it do?
This app lets a user find the cheapest (or most expensive) food item of their searching. Simply enter a food item into the search bar, look through the list of options and/or find them on the map!

<br />

## What did you build it with?
* Frontend built using React as a View layer, Webpack as a module bundler and SASS as a css-preprocessor
* HTML5 Geolocation API
* Foursquare API
* Google Maps API
* Axios - HTTP client

<br />

## How do I run it locally?
This repo uses yarn as a package manager. [Yarn can be installed using homebrew.](https://yarnpkg.com/en/docs/install)

1. Clone repo locally
2. Run `yarn install` to install all dependencies
3. Run `yarn start`
4. Navigate to [http://localhost:3000/](http://localhost:3000/)

<br />

## How does it work?

I initially use the HTML5 Geolocation API to get the user's location on the `<App />` component's componentDidMount lifecycle method. I then use the Foursquare API to fetch a list of restaurants. Once the response is received, I traverse through the data to extract the menu data along with some basic information about the restaurant and set this to the state (`this.state.menuData`). Once a user searches for a food item in the input, I search through all restaurant menus to check if their name or description contain the input value and set these food items on the state (`this.state.foodItems`) along with some basic information about the restaurant. `this.state.foodItems` is then passed as a `prop` to the `<Map />` component, which maps through each food item and renders a `<Marker />` for each.

<br />

## Thoughts and Considerations

In order to create an app that allowed a user to search for a food item within a given radius, I needed menu data. Unfortunately, the Google Places API did not have sufficient menu data and due to a lack of time I decided to use the Foursquare API to retrieve this data. I do realize the instructions stated to use the Google Places API; however, I felt inspired that this app would do an excellent job of demonstrating my skill set and abilities, so I opted to make a minor tweak and use the Google Maps JavaScript API instead. I do hope this isn't an issue.

<br />

One of the biggest issues with the app is the Foursquare API endpoint for venues. At the time of development, there was not an endpoint that returned a list of ALL venues within a given radius.

The "Search Venue" endpoint takes an `intent` parameter. The most relevant values to pass it are `checkin` and `browse`. Here's what they each do:

`checkin`: Finds results that the current user...is likely to check in to.

`browse`: Finds venues within a given area. Unlike the checkin intent, browse searches an entire region instead of only finding Venues closest to a point.

So there's basically no way to search for a list of all venues closest to you that use Foursquare...seems to be a big feature to exclude from their API.

When doing a regular search on the foursquare.com website for "food" closest to my current location, I get a different list than the one that returns from my API call to their "Search Venue" endpoint. So when you're searching for a food item on Dish, you're only searching through a handful of the venues around you that use Foursquare, not all of them (plus, there's a limit of 50 venues returned and some don't have menus uploaded).

After digging into stackoverflow, I found that I wasn't the only one experiencing this issue:

[Case 1](https://stackoverflow.com/questions/16581038/why-does-foursquare-search-not-return-venues-closest-to-my-specified-location)

[Case 2](https://stackoverflow.com/questions/33302515/foursquarevenues-searchintent-browse-returns-more-places-when-specifying-categ)

Conculsion: If you feel like the search doesn't return as many options as you'd think it would, this is why. If I were to add features to this app, I would look into using the [Locu API](https://dev.locu.com/) or Yelp API in replacement.

<br />

## How could it be improved?

* ~~Handle user error form submit~~
* ~~Add responsiveness~~
* ~~Add zoom button to map~~
* Redux for state management
* Show ratings for each restaurant
* Show distance from restaurant
* Sort by distance
* Get directions to restaurant
* Save food items
* Expand search radius
* Make searching algorithm more complex (handle plurals)
* Display modal if geolocation api fails
* Unit tests
* Add in ability to click on marker and item will show in list
* Search dropdown with previously searched
* Use different API for more accurate venue searching