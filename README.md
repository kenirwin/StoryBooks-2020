# StoryBooks-2020

In 2018, Brad Travery published *Node.js, Express and MongoDB Dev to Deployment* with Packt Press. In the time since it was published, some features of the Node.js landscape have changed, and the code he originally wrote needs a few tweaks to function. The original published code is available at https://github.com/PacktPublishing/Node.js-Express-and-MongoDB-Dev-to-Deployment

The changes presented here are based on the source code from Chapter 8.7.

## What changed?

### Updates to MongoDB cloud hosting

mLab has been absorbed by MongoDB, and the version of MongoDB has a slightly different database-connection structure than that of the older version. The current MongoDB connection uses the **mongodb+srv://* protocol, which is not supported under the version of Mongoose used in the original code. The version presented in this repo updates the Mongoose version to accommodate.

### Different Mongoose.connect() options

THe move to a new Mongoose version requires a few changes to the Mongoose.connect() options; this repo makes those changes (which a person could do by reading the console.log and following the error messages in the original code.

### Changes in handling of local variables

Chapter 8 includes the addition of this code block to define a local `user` variable based on the results of a database call at login time:

```
// Set global vars
app.use((req, res, next) => {
  res.locals.user = req.user || null;
  next();
});
```
The current version of ``express-handlebars`` gives an error message when that `user` object's properties are called from within handlebars. That error can be resolved by installing handlebars 4.5.3 as a dev dependency: `npm install handlebars@4.5.3`; that solution was described at :
https://stackoverflow.com/questions/59690923/handlebars-access-has-been-denied-to-resolve-the-property-from-because-it-is

This last issue stopped me in my tracks for several hours, and led me to write up this solution.