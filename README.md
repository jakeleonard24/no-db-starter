# no-db-starter

## Project Summary
The no-database project is your first major project here at DevMountain. It is your first opportunity to bring together the various skills you've learned and demonstrate how much you've already learned and grown.

It is important to remember that this is first and foremost a learning experience. Your application will not be perfect. Set a high bar for yourself, but don't expect this app to revolutionize an industry or be the best at this or that thing. The major projects at DevMountain (NoDB, personal, group) are probably the biggest learning experiences you'll go through during your time here. 

This Repo is going to cover these steps in order to get your started:
  * Create-React-App
  * Setting Up A Server File
  * Running Nodemon
  * Writing a basic axios call
  * Building the corresponding Endpoint

* ***Create React App*** - By now you should hopefully have `create-react-app` installed but just in case you haven't or it was removed. run `npm i -g create-react-app`.  Then when that is finished cd into the folder where you want to create your new app and run. `create-react-app name` in place of name type whatever you want to name your new project.  Note that `create-react-app` will create a folder named whatever you specified with a basic react app inside of it. Once create-react-app finished, cd into the project directory and run `npm start`.

* ***Setting Up Server File*** - Create your server file by first creating a folder called server in the root of your project folder called `server` .  Inside that server folder create a file called `server.js` .  Open up your server.js file. You will need to install three dependencies, for this file: express, body-parser and cors.  To do this open up your terminal, make sure you are in your project directory, and run either `npm install express body-parser cors` or `yarn add express body-parser cors`.  

You will then need to import those dependencies in your server.js file. 
   ```
    const express = require('express')
    const bodyParser = require('body-parser')
    const cors = require('body-parser')  
   ```
   
 You will then need to use those imported dependencies. 
 
 ```
 const app = express();
 app.use(bodyParser.json());
 app.use(cors());
 ```
 
 Now it is time to specify what port you want your server running on and get it listening on that specific port.  To do this create variable `port` and set it equal to a number like `3333`.  The use the app.listen method to set the server listening on that port. It should look something like this.
 ```
 const port = 3333
 app.listen(port, () => console.log(`listening on port ${port}`));
 ```
 These are the basic steps to getting your first server built and running!
 
 * ***Running Nodemon*** - Now in order to make that server functional we need to run nodemon. Nodemon is a utility that will monitor for any changes in your source and automatically restart your server. Which is awesome for development! If you haveen't installed nodemon the command is `npm i -g nodemon` . 
 
 Once nodemon is installed you need to get it running in your server file.  You could do this buy running `server/server.js` from your project directory.  Another way to do this which will make your life easier in the future is to open up your package.json file and underneath the property private insert the line 
 ```
 "main":"server/server.js",
 ```
 Then in the terminal run `nodemon`.
 
 * ***Making A Simple Axios Call*** - It's time to get our front end talking to our back end!  Create-react-app builds a shell App component for you, but for this component we will need state.  Add a constructor, super, and state to your component so that when we make our axios call we can save that information.  It should look something like this:
 ```
 class App extends Component {
  constructor(){
    super()
    this.state = {}
    }
  ```
 Now lets use a lifecycle method to run our `axios.get` as the page loads.  The lifecycle method we want to use here is `componentDidMount()` this will run anything inside the method everytime the page reoloads.  Write the `axios.get` inside the `componentDidMount()` method.  It should look like this: 
 ```
 componentDidMount(){
  axios.get('http://localhost:3333/api/test')
  .then(response => {
    this.setState({
      picture: response.data
    })
  })
}
```

* ***Building The Correponding Endpoint*** - Now we need to build an endpoint to receive the axios call that we are making on our front end.  This endpoint will take in information sent in the request and use it to perform a task.  In this case we want it to get some data and send it back to our front end so we want our endpoint to be a get endpoint and start with `app.get`. The URL of this endpoint will need to match what we had in our axios call or vice-versa.  And inside the callback of the endpoint we want to specify what exactly the get request will send back to the front end.  It should look like this: 
```
 app.get('/api/test', (req, res)=> {
     res.status(200).send('http://i63.tinypic.com/2j9y8p.png');
 })
```
Now, when viewing our app on localhost:3000, as the page reloads we are making an axios call to our database and it is sending us back some information, in this case, a picture.

Good luck and happy coding!

