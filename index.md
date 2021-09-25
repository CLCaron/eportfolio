## Welcome to Christopher Caron's ePortfolio!

# E-Commerce Demo
**[View on GitHub](https://github.com/CLCaron/e-commerce-demo)**

# What is it?
This is a an e-commerce demo website where a user can register an account (or sign in with Google), add items to their cart, and "pay" for the items in checkout. There are no real monetary transactions taking place as the checkout is completed using a test credit card number for Stripe.

# How was it made?
This website was built using React and Node.js. It is currently utilizing Redux and Redux-Sagas. Firebase is used to handle user logins via e-mail address or sign-in with Google and store their account information. A backend has been built using express which is currently only used for Stripe payment transactions. Other modern libraries were used and a full list can be found at the bottom of this ReadMe.

# Capstone Enhancements
This project is being used for my computer science capstone. Enhancements will be made to demonstrate understanding in the following three categories:

Software Design/Engineering
Data Structures and Algorithms
Databases

Software Design/Engineering and Databases will be fulfilled by the new orders page that has been implemented. If a registered user places an "order," the order information will be stored in MongoDB. The user can visit the "Orders" page and view any order history.

Data Structures and Algorithms will be fulfilled by implementing a manual quicksort function to sort items by price. 

# Code Review
**[View on YouTube](https://youtu.be/C7BVQWipZbc)**

# Images:
![homepage image](https://imgur.com/78UPZvX.jpeg)
![checkout image](https://imgur.com/hMPltr9.jpeg)
![orders image](https://imgur.com/Y8rbSvX.jpeg)

# Libraries and technologies used:
**[Axios](https://axios-http.com/)**: "A promise based HTTP client for the browser and node.js"

**[Express](https://expressjs.com/)**: "Fast, unopinionated, minimalist web framework for Node.js"

**[Firebase](https://firebase.google.com/)**: "A platform developed by Google for creating mobile and web applications."

**[Lodash](https://lodash.com/)**: "A modern JavaScript utility library delivering modularity, performance & extras."

**[MongoDB](https://www.mongodb.com/)**: "The most popular database for modern apps"

**[Node.js](https://nodejs.org/en/)**: "Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine."

**[React](https://reactjs.org/)**: "A JavaScript library for building user interfaces"

**[Redux](https://redux.js.org/)**: "A Predictable State Container for JS Apps"

**[Reselect](https://github.com/reduxjs/reselect)**: "Simple “selector” library for Redux (and others)"

**[Sass](https://sass-lang.com/)**: "Sass is the most mature, stable, and powerful professional grade CSS extension language in the world."

**[Styled Components](https://styled-components.com/)**: "Visual primitives for the component age."
