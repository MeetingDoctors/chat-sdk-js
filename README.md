This project was bootstrapped by MeetindDoctors on top o a [Create React App](https://github.com/facebook/create-react-app).

# Available integration options

This SDK consist in a Vanilla JS library that will, ultimately, render the MeetingDoctors web client on the integrators page.

For the integrator it will be necessary to integrate the JS, and also a custom CSS file to override the applied styles.

## `JavaScript`
#### `- <script src=widged.meetingdoctors.com/Vx.x.x/main.js />`

The first option to import the JS would be to insert a scrtipt on the HTML document pointing to the aimed version.
This would expose a new object (the library) attached at the Window object

You can call the methods then, in the following way

```javascript
<script>
window.meetingDoctors.initialize({...args});
...
</script>
```

See below the definition of those args

<!--Where mountPoint indicates the div into which the application will be displayed.-->
<!--If no mountPoint is given, the application will render in the fullScreen mode-->

<!--jwt will be the JWT obtained by the integrator in order to initialize the session of the user-->
<!--to obtain the JWT the integrator will have to previously authenticate the user against meetingDoctors.this can be done from a server2server call, or enabling new registers from the client.-->


#### `- Universal Module Declaration`
If you download the package via a Package Manager like NPM, you can then require the module into your own JS

```javascript
// ES6
import meetingDoctors from "MeetingDoctors"

// ES5
var meetingDoctors = require("MeetingDoctors")
```
Then you can call any method on the library like
```
meetingDoctors.initialize({...args});
...
```
See below the definition of those args


## `Library API`

### Args
Args will be an object with the following defined keys, this object will be interpreted in the Initialize method and will trigger the execution of the SDK

#### containerId
containerId 'string' : indicates the Id of the doom element in which you want to render the app. If no contaierId is provided, the application will be rendered in FullScreen mode

#### JWT
jwt 'string' : is the JWT provided by meetingDoctors af a particular user.
Using this JWT the whole library will authenticate as said user
There are many ways to obtain the WJT, depending on the integration strategy.

### Methods

#### `initialize({ jwt , containerId })`

The initialize function will trigger the Render of the meetingDoctors app
This method will internally call the two following ones

#### `authenticate(jwt)`

The authenticate function will take a jwt and use it to initialize against all the services of meetingDoctors. This way, the SDK can connect with the notifications and chat service.

#### `mount(containerId)`

Once you have authenticated the widget, you can render it inside any element of your DOM that has a given width and height, and an Id(unique) to reference it.
Depending on the dimensions of said element, the widged will be rendered as partial views or full view.



## `Styles`

The SDK provides some of the styles for a proper render of the Chat, but it is just a default styling of the chat.

The integrator can also add an upper layer of CSS to override the styles and customize to deliver the same look & feel than the rest of the page.

An initial template of the customizable CSS classes will be provided with the package installation.
