Ember Data Adapter for Parse
============================

An [Ember Data Adapter](https://github.com/emberjs/data) built to use the [Parse REST API](https://parse.com/docs/rest). This is a full Ember implementation against the Parse REST API without the use of the Parse JavaScript SDK. It is implemented against [revision 11](https://github.com/emberjs/data/blob/master/BREAKING_CHANGES.md) of the Ember Data framework.

Features
--------

##### ParseConnector: Ember Mixin
  * Provides the AJAX connectivity to the Parse REST API.
  * CORS implementation

##### ParseJSONSerializer: Ember Data JSONSerializer
  * Provides the translation of objectId to id for identity mapping.
  * Provides encoding of hasMany associations to [Parse Pointer objects](https://parse.com/docs/rest#objects-types).
  * Provides batch serialization according to [Parse batch operations](https://parse.com/docs/rest#objects-batch).
  * Serializes Date types to the [ISO 8601 as used by Parse](https://parse.com/docs/rest#objects-types).

##### ParseAdapter: Ember Data Adapter
  * Implements the persistence layer to Parse.
  * Provides either bulk/batch persistence or granular (bulkCommit by default).

##### ParseMixin: Ember Mixin
  * Provides created/updated date attributes.

##### ParseModel: Ember Data Model
  * Provides an easy way to setup a Parse object.
  * Includes new StateManager that includes Parse specific states (Password Reset)

##### ParseUser: Parse User implementation.
  * Login
  * Signup
  * Request password reset

Get Started
-----------
First take a look at the example.html file in the root of this project. It includes a very basic implementation of an application. Read the source to understand how the Ember Data Adapter for Parse is configured. You will want to include your Parse acct information from [Parse](https://parse.com) and then you can run that example.html file in a browser.

Or if you prefer to jump right in, grab the latest version of ember-parse-adapter from the /dist directory in this project and include it in your HTML after the Ember dependencies.

```html
<!-- dependencies -->
<script src="vendor/jquery.min.js"></script>
<script src="vendor/handlebars-1.0.0-rc.3.js"></script>
<script src="vendor/ember-1.0.0-rc.1.js"></script>
<script src="vendor/ember-data.js"></script>

<!-- Parse Data Adapter (latest build) -->
<script src="dist/ember-parse-adapter-0.2.2.js"></script>
```

Next you'll want to get an account at [Parse](https://parse.com). After this you will be provided with three keys:

* Application ID
* JavaScript Key
* REST API Key

You will need each of these to configure the ParseAdapter.

```javascript
  var App = Ember.Application.create();

  App.ApplicationAdapter = ParseAdapter.extend({
    applicationId: '<YOUR APP ID HERE>',
    restApiId: '<YOUR REST API KEY HERE>'
  });
```

Once you have your adapter configured now you can create ParseModels just as you would create DS.Models.

```javascript
  App.Post = ParseModel.extend({
    title: DS.attr('string'),
    body: DS.attr('string')
  });
```

Issues
------

* Demo is not out-of-the-box due to Parse acct dependency.
* findQuery implementation is a bit weak/brittle. Needs full [Parse Query](https://parse.com/docs/rest#queries-constraints).
* Error conditions are handled only by logging the error.

Roadmap
-------

* Parse Roles implementation
* Parse ACL implementation
* Parse Relation for many-to-many associations.
* Implement Store record error states.
* Implement full type encodings in ParseSerializer supported by Parse (Bytes/Pointer/Relation).

Dev Notes
---------
* To get a build simply grunt. You'll find builds inside the /dist folder.
