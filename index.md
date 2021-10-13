## Welcome to Christopher Caron's ePortfolio!

# Professional Self-Assessment
During my time at SNHU, I have learned a lot about computer science, and software engineering, specifically. I have gained a deep understanding of computer science’s role in a variety of industries. I have also learned a lot about databases, Linux, object-oriented analysis and design, data structures and algorithms, the software development lifecycle, testing, quality assurance, automation, reverse engineering, mobile programming, secure coding, data mining, and client/server development. There were many courses that helped me gain a deep understanding on these topics and in my capstone course, I was able to make three enhancements for an existing project which I completed outside of coursework. I was able to create this project and its enhancements due to my education at SNHU. 

My project required a deep understanding of databases to store customer and item data and client/server development to create a front-end and back-end that could properly communicate with each other. My enhancements allowed me to demonstrate an understanding of software design/engineering, algorithms and data structures, and databases by creating brand-new features. One of these features involved software design/engineering and database work to complete a page that allows a user to view orders that they have placed. Another feature required knowledge of algorithms and data structures to allow a user to sort items by price using a manually written quicksort method. All of this work showcases what I have learned at SNHU.


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

# Enhancement One
An Orders page was created! An image can be viewed below. Note: This enhancement involved working with MongoDB to become fully functionality. The details regarding the work with MongoDB can be found under Enhancement Three

This enhancement involved the following:

* Creating a new Orders page component, under the pages directory
* Creating a route to the Orders page in App.js
* A link to click on for the Orders page in the header
* Creating an Order component that can be reused on the Orders page, in the components directory. The order info to be displayed in this component is passed in from the parent component (Orders), where React Hooks are used in conjunction with the Axios library to fetch the order data (stored in MongoDB)
*  Giving the Orders page access to the currentUser object using Redux selectors so that the user's firestore ID can be stored in MongoDB (orders are tied to a Firestore ID as sign-up/sign-in/authentication is handled with Firebase until a full migration to MongoDB)
*  Mapping over the retrieved orders only once upon the Orders page being loaded and returning an Order component for each order, to be displayed on the Orders page
*  Implementing Axios to make requests to the Express server, and connecting to MongoDB in server.js

This enhancement was created because any online store needs an “orders” page. If a customer is placing an order, they should be able to review that order in the future. I felt that this was a great exercise to perform. I believe that the knowledge required for this enhancement showcases my understanding of software engineering/design. This enhancement involved understanding a database as well as connecting that database to an application and using the data. I needed to make an entirely new page for a user to visit with entirely new functionality, new React components, and new technologies/libraries to complete this enhancement.

# Enhancement Two
A quicksort function was written and replaced the default ".sort()" JS function that was previously being used for sorting items on a collection page!

This enhancement involved an understanding of data structures and algorithms. I needed to understand how arrays work, how to use the data in the array, recursion, and the logic for sorting the data. The full code for this quicksort can be seen below:

<pre><code>  const swap = (items, leftIndex, rightIndex) => {
    let tmp = items[leftIndex];
    items[leftIndex] = items[rightIndex];
    items[rightIndex] = tmp;
  };

  const partition = useCallback((items, left, right) => {
    let pivot = items[Math.floor((right + left) / 2)].price, // This gives us the middle element
      i = left, // This is the left pointer
      j = right; // This is the right pointer

    while (i <= j) {
      while (items[i].price < pivot) {
        i++;
      }

      while (items[j].price > pivot) {
        j--;
      }

      if (i <= j) {
        swap(items, i, j); // This is what actually swaps two elements.
        i++;
        j--;
      }
    }

    return i;
  }, []);

  const quickSort = useCallback(
    (items, left, right) => {
      let index;
      if (items.length > 1) {
        index = partition(items, left, right); // This is the index that is returned from partition

        if (left < index - 1) {
          // Check if more elements on left side of the pivot
          quickSort(items, left, index - 1);
        }

        if (index < right) {
          // Check if more elements on the right side of the pivot
          quickSort(items, index, right);
        }
      }

      return items;
    },
    [partition]
  );</code></pre>
  
This enhancement was created because I believe any online store should allow a user to sort items by price. Much like my decision for the software engineering/design enhancement, I felt that this was a great exercise because it is similar to a real-world scenario enhancement. More importantly, I feel that this enhancement demonstrates my understanding of data structures and algorithms quite well. I needed to understand how arrays work, how to use the data in the array, recursion, and the logic itself for sorting. There is a lot going on in my quicksort method, as can be seen above.

# Enhancement Three
MongoDB was implemented and create/update and read operations were implemented! This enhancement ties in a bit with enhancement one, as enhancement one needed these database operations to be fully functional.

This enhancement involved the following:

* Installing MongoDB
* Connecting the database to the existing application
    * Modified server.js to use mongoose.connect, db.on to log any error, and db.once to log "Connected to database..." only ONCE after successfull connection
* Creating a User model/schema with an array of orders
    * Created a user.js file in a new "models" directory which models the user: firestoreID, name, email, address, array of orders 
* Writing queries for inserting/updating and reading from the database
    * Created a users.js file in a new "routes" directory.
        - Wrote a getUser function using MongoDB's findOne operation and passing in firestore ID from the req params
        - Wrote a function (currently unused) to retreive all user documents from the DB
        - Wrote a function to retreive one user's orders, utilizing the getUser function and res.json that user's orders
        - Wrote a create/update function which creates an address object from the Stripe payment token from the request, an order (orderID generated with UUID, orderDate, orderedItems, total, customerName, customerEmail, and address set to the previously created address object) from the body and token in the request. Utilizes findOneAndUpdate on the User model. Finds user by firestoreId. If the user exists, the order in the request will be pushed onto the document's orders array. If the user does not exist, a new user with the new order and their Firestore ID will be created. This was accomplished using MongoDB's upsert flag.
    * Integrated this database code with the Express and Axios libraries as mentioned in Enhancement One so that orders can be displayed in the Orders page
    
This enhancement was accomplished alongside enhancement one. It was necessary to create a database with create, read, and update operations to complete enhancement one. As stated in the reflection of enhancement one, this enhancement involved an understanding of databases. I needed to understand how to use MongoDB by installing it and implementing it in my application as well as writing a schema with the create, read, and update operations which are performed via GET and POST requests. None of this would be possible without an understanding of databases, so I feel that this demonstrates my knowledge on this subject quite well.

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
