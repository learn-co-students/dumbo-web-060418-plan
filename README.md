# Dumbo Web 060418 Project Mode Plan

## One Big Rule
The biggest advice we can give you for project mode is to scope your project idea down! Make the tiniest MVP possible and have a lot of stretch goals. Build new features onto your MVP iteratively. That is the way to build a great product.

## The Secret of Life is Good Git
- Create branches for each feature you add (e.g. add-user-functionality)
- Commit frequently to your branch
- From your branch make a pull request against master and merge the work in
- Delete the branch
- If you use this workflow, your master branch should always be in a good working state.
 
## Thursday Planning
On Thursday, take some time with your group to plan out the following areas of your project. Doing this before you start coding will make later steps much easier.
  - What are your backend routes
	- What are your models
  - What are your user stories (what should a user be able to do with your app)
	- Take time to wireframe the frontend
	- Map out your React component hierarchy
	- Where do props and state live
	- What is MVP
	- What are stretch goals

## Daily Standups
The entire class will participate in a full-group standup at 9:30am on Thursday and Friday. This is a place for you to share your ideas/problems and seek help or guidance. Each group should answer these 3 questions in their standup.

1. What is the last feature built?
2. What is the next feature to be built?
3. If your project was a sound, what would it sound like?

## Project Requirements

You've been through quite a few Project Modes by now and should have some idea how to think about scoping a project, what you can accomplish in a the designated time, and what is expected of you in terms of meeting complexity requirements.

The guidelines here are minimal but be sure that you:

1. Use a _Rails API backend_ with a separate _React frontend_ that are created in two different Github repositories.
2. Have at least three resources on the backend and your application must have full CRUD actions for at least one resource.
3. React Router is not required. You can build a single-page application.
4. Do not implement authorization. ***MORE HERE***

It is highly suggested that any calls to 3rd party APIs are made _through your backend_.

Example: A user clicks a button that says 'Get Gifs'
* React makes a request to Rails
* Rails makes a request to the Giphy Api
* Rails receives the response from Giphy and sends to React
* React receives the response from Rails and you do something with it on the client

This is so you can avoid any *CORS* issues. If you are unable to hit an API from your React app due to a CORS restriction, it is very likely that it is impossible to do so. _Brief Refresher on CORS: the idea is that from one domain (the port your webpack development server is running on) you are not allowed to access another domain.  You must make the request from a server (i.e. Rails), so the request is exempt from the Same-Origin Policy restriction._


## Backend Setup
```
rails new <my-project> --api -T --database=postgresql
```

Let's go through this in detail:

* `--api`
  *  Make a [Rails 5 API](http://edgeguides.rubyonrails.org/api_app.html), basically you're telling Rails you don't want any of the stuff you wouldn't need for an application where Rails is not rendering views. Think the ActionView library (`form_for`, `link_to`, etc..), ERB, Security protections that ensure forms were rendered by the Rails app, things like that.
* `-T`
  * don't generate tests for this app
* `--database=postgresql`
  * Set this up to use a Postgres (as opposed to SQLite) database. If you ever want to push this to Heroku, Heroku requires a Postgres database. There won't be too much difference in how you have to write your code. You'll have to be sure to run `rails db:create` and make sure you have postgres running (i.e you can see the elephant)
* Be sure to do the necessary setup for the [rack-cors-gem](https://github.com/cyu/rack-cors)
* You may want to use [active-model-serializers](https://github.com/rails-api/active_model_serializers/tree/0-10-stable)

## Frontend Setup
To create your React project, you may use a tool called [create-react-app](https://github.com/facebookincubator/create-react-app), an awesome project generator developed by Facebook. To use this
+ `npm install -g create-react-app` - this installs the generator as a global package
+ In the directory where you'd like to create your project, `create-react-app my-project-client`. It's that simple!

We'd reccommend to begin by removing any of the default stuff given to you by Create React App that you do not understand. The following are some really great resources on how to think about setting up a React project (_Spoiler: They both say the same thing, "There's no right answer!"_)
* [React Docs](https://github.com/reactjs/reactjs.org/blob/71788c647daa07392a8156609fdbede8e9ed24f7/content/docs/faq-structure.md) This was written by Dan Abramov himself <3 <3 <3....
* [The 100% Correct Way to Structure a React App (or why there’s no such thing)](https://hackernoon.com/the-100-correct-way-to-structure-a-react-app-or-why-theres-no-such-thing-3ede534ef1ed)

## Notes
By default both your client app and your rails app will run on port 3000. You'll have to specify one or the other to run on a separate port.
* Rails: `rails s -p <some_number_thats_not_3000>`
* React: Check out this [issue](https://github.com/facebookincubator/create-react-app/issues/1083)

A great article on how [DHH thinks about setting up controllers in Rails](http://jeromedalbert.com/how-dhh-organizes-his-rails-controllers/)
