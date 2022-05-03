# 21 MERN: Book Browser

## Summary

Book Browser is built using the MERN stack with a React front end, MongoDB database, and Node.js/Express.js server and API with a fully functioning Google Books API search engine built with a RESTful API, and refactor it to be a GraphQL API built with Apollo Server.

## Getting Started

In order for this application to use a GraphQL API, you’ll need to refactor the API to use GraphQL on the back end and add some functionality to the front end. The following sections contain details about the files you’ll need to modify on the back end and the front end.

### Back-End Specifications

You’ll need to complete the following tasks in each of these back-end files:

- `auth.js`: Update the auth middleware function to work with the GraphQL API.

- `server.js`: Implement the Apollo Server and apply it to the Express server as middleware.

- `Schemas` directory:

  - `index.js`: Export your typeDefs and resolvers.

  - `resolvers.js`: Define the query and mutation functionality to work with the Mongoose models.

  - `typeDefs.js`: Define the necessary `Query` and `Mutation` types:

    - `Query` type:

      - `me`: Which returns a `User` type.

    - `Mutation` type:

      - `login`: Accepts an email and password as parameters; returns an `Auth` type.

      - `addUser`: Accepts a username, email, and password as parameters; returns an `Auth` type.

      - `saveBook`: Accepts a book author's array, description, title, bookId, image, and link as parameters; returns a `User` type. (Look into creating what's known as an `input` type to handle all of these parameters!)

      - `removeBook`: Accepts a book's `bookId` as a parameter; returns a `User` type.

    - `User` type:

      - `_id`

      - `username`

      - `email`

      - `bookCount`

      - `savedBooks` (This will be an array of the `Book` type.)

    - `Book` type:

      - `bookId` (Not the `_id`, but the book's `id` value returned from Google's Book API.)

      - `authors` (An array of strings, as there may be more than one author.)

      - `description`

      - `title`

      - `image`

      - `link`

    - `Auth` type:

      - `token`

      - `user` (References the `User` type.)

### Front-End Specifications

You'll need to create the following front-end files:

- `queries.js`: This will hold the query `GET_ME`, which will execute the `me` query set up using Apollo Server.

- `mutations.js`:

  - `LOGIN_USER` will execute the `loginUser` mutation set up using Apollo Server.

  - `ADD_USER` will execute the `addUser` mutation.

  - `SAVE_BOOK` will execute the `saveBook` mutation.

  - `REMOVE_BOOK` will execute the `removeBook` mutation.

Additionally, you’ll need to complete the following tasks in each of these front-end files:

- `App.js`: Create an Apollo Provider to make every request work with the Apollo Server.
- `SearchBooks.js`:

  - Use the Apollo `useMutation()` Hook to execute the `SAVE_BOOK` mutation in the `handleSaveBook()` function instead of the `saveBook()` function imported from the `API` file.

  - Make sure you keep the logic for saving the book's ID to state in the `try...catch` block!

- `SavedBooks.js`:

  - Remove the `useEffect()` Hook that sets the state for `UserData`.

  - Instead, use the `useQuery()` Hook to execute the `GET_ME` query on load and save it to a variable named `userData`.

  - Use the `useMutation()` Hook to execute the `REMOVE_BOOK` mutation in the `handleDeleteBook()` function instead of the `deleteBook()` function that's imported from `API` file. (Make sure you keep the `removeBookId()` function in place!)

- `SignupForm.js`: Replace the `addUser()` functionality imported from the `API` file with the `ADD_USER` mutation functionality.

- `LoginForm.js`: Replace the `loginUser()` functionality imported from the `API` file with the `LOGIN_USER` mutation functionality.
