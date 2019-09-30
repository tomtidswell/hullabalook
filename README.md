# Hullabalook code test

# Brief
A member of the Sales team has just got back from a meeting with a potential new client. The client has asked if we could create an interactive experience for their online customers. The purpose of the experience is to inform their most loyal customers of the variety of brands they sell.

They want us to create a pairing game whereby the user is faced with four product images and four brand logos, and they need to match the product to the brand logo.

# Author's note

* I spent one day working on this app
* I met all of the requirements
* This is the first time I have built a Vue app unaided, so I am very proud of my achievement!
* There is no test suite installed for this as I used my time up just creating the app


# Installation and testing
1. Download or clone the repository to your local machine from github

2. Grab the packages from yarn
```
yarn
```
3. Serve it to localhost
```
yarn serve
```
4. If the dev server doesnt open your browser automatically, [launch the localhost](http://localhost:8080)

It's ready to use.

## Informal Testing

Once the project has loaded, simply click the start button to initiate the timer. The objective is then to match all the trainers within 30 seconds.


# Key Features
* I demonstrated use of many different parts of Vue capability: multiple components, conditional rendering, computed properties, transitions, scoped styling
* It is responsive (with some tweaks needed)
* It is extensible. If the data array is extended, the app will display the game accordingly


# Future improvements
* Add additional trainers and product types
* Improve the incorrect choices so that they are remembered when clicking between products

# Bugs
* The animations can seem a little glitchy when clicking between products
* The interface seems a little sparse, so the design should be improved
* When the browser is tablet sized the tiles can cut off to the right - this behaviour is ok on mobile but is awkward wihtout touch to scroll right
