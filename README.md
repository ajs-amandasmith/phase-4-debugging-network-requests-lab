# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
    - Clicked on the Add a Toy button
    - Filled in some data for the inputs
    - Clicked Create a New Toy button
    - Looked at console error message (Internal Server Error)
    - Looked at Network response
      - Saw the 500 Status code (Internal Server Error)
      - Looked at the Network Preview
        - Saw "NameError: uninitailized constant ToysController::Toys" exception
    - Looked at the server log
      - Saw the same error from the preview and also saw where the error was exactly (app/controllers/toys_controller.rb:10:in 'create')
    - Updated "Toys.create" to "Toy.create"


- Update the number of likes for a toy

  - How I debugged:
    - Clicked "like" on a toy
    - Read the error in the browser (SyntaxError): Unexpected end of JSON input
      - Same error in the console
    - Checked the Network debugger tool and couldn't figure that out
    - Refreshed page
    - Read the logs from the two terminals
    - 204 No Content error - app/controllers/toys_controller.rb:16:in 'update'
    - checked the controller file
    - saw there was no json being rendered
    - added the render json
      - need to find what the status should be when something was updated



- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
    - Clicked a donate to goodwill button on a toy
    - Looked at the console error (404 Not Found)
    - Looked at network preview (ActionController::RoutingError: No route matches delete)
    - Looke at terminal logs
    - checked the controller, didn't notice anything
    - checked the routes and saw there wasn't a destroy listed in the resources
    - added that
