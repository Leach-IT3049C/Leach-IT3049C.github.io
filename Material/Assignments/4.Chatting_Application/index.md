---
layout: default
title: 4. Chatting Application
parent: Assignments and Labs
has_children: false
published: true
nav_order: 4
---
---
# 4. Chatting Application (Lab)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This lab, you will be following the instructions and to build a chatting application that we can use as a class.
For most of the parts, I have provided snippets of code for you to use.
> Make sure your understand those snippets for your own sake, as well as for future assignments.

## Lab Goals
1. Build a simple chatting application using HTML, CSS, and JavaScript.
2. Demonstrate ability to use Bootstrap to setup the page layout.
3. Demonstrate ability to create forms with the form/input elements.
4. Demonstrate understanding of event-oriented programming.
5. Demonstrate understanding of JSON objects, Web Request, and the Fetch API.

### Tips and Guidelines
* commit your code frequently.
    * the <img alt="commit logo" style="height: 15px;" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Octicons-git-commit.svg/1200px-Octicons-git-commit.svg.png"/> icon usually indicates a good checkpoint for a commit.
    * Use useful commit messages.
* Make sure tests pass.
    * `✅ ++` usually indicates that another tests should pass at this point.
* **Don't forget to fill out the self assessment on the README file**.

## Layout Instructions
### Setup
1. Accept the assignment on canvas.
  This will create a repository for you with a few starting files.
    ```
    .
    ├── resources
    │   ├── images
    │   │   └── .gitkeep
    │   ├── scripts
    │   │   └── index.js
    │   └── styles
    │       └── styles.css
    ├── index.html
    └── README.md
    ```
2. the `index.html` file includes
    * a title of `IT3049C-Chat`
    * a link to the styles sheet in `resources/css/styles.css` - For out custom styles.
    * a link to the script file in `resources/js/index.js` - For our custom scripts.
    * a link to Bootstrap styles and scripts. - For a responsive design with better ascetics
    * a link to FontAwesome styles. - for icons

    <details>
    <summary markdown="span">
        <strong>The starting html page should look like this</strong>
    </summary>
    ```html
    <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="UTF-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <title>IT3049 Chat</title>
            <!-- Bootstrap + JQuery + FontAwesome -->
            <link rel="stylesheet" href="resources/vendor/bootstrap.min.css" />
            <script src="resources/vendor/jquery-3.5.1.slim.min.js"></script>
            <script src="resources/vendor/popper.min.js"></script>
            <script src="resources/vendor/bootstrap.min.js"></script>
            <link rel="stylesheet" href="resources/vendor/fontawesome-free/css/all.min.css" />
            <link rel="stylesheet" href="resources/css/styles.css" />
        </head>

        <body>
            <header>

            </header>

            <div id="chat">

            </div>

            <footer>

            </footer>
            <!-- Our own Scripts -->
            <script src="resources/js/index.js"></script>
        </body>
    </html>
    ```
    </details>

### Header/Jumbotron
1. Inside the `<header>`, Add a [Bootstrap Jumbotron Header](http://getbootstrap.com/docs/4.5/components/jumbotron/). 
    ```html
    <div class="jumbotron">
        <h1 class="display-4">IT-3049C Chat</h1>
    </div>
    ```
* Notice both `jumbotron` and `display-4` are bootstrap classes.
* ✅ ++

2. In the jumbotron div, create an input field for the name.
    * input needs to have an id of `myName`
    * input will have a placeholder of *Name*
    * input field will be part of [bootstrap input group](https://getbootstrap.com/docs/4.5/components/input-group/).
        * the group constains the input itself and [icon representing a user](https://fontawesome.com/icons/user?style=solid)

    ```html
    ...
    <div class="input-group mb-3">
        <div class="input-group-prepend">
            <span class="input-group-text">
                <i class="fas fa-user"></i>
            </span>
        </div>
        <input id="myName" type="text" class="form-control" placeholder="Name">
    </div>
    ...
    ```
    * *Tip*: You may want to hard-code your name into the input value, so you don’t have to type it in every time you refresh the page 😉 
        ```html
        <input id="myName" ... value="Ben Leach">
        ```
> Now the page  div should look like this
<img alt="a page with a jumbotron and input field" src="assets/1.png" style="width:100%; border:1px #ddd solid;"/>

<details>
<summary markdown="span">
    <strong>and the html code should look like...</strong>
</summary>
```html
<header>
    <div class="jumbotron">
        <h1 class="display-4">IT-3049C Chat</h1>

        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text">
                    <i class="fas fa-user"></i>
                </span>
            </div>
            <input id="myName" type="text" class="form-control" placeholder="Name">
        </div>
    </div>
</header>
```
</details>

### Application Chat input
1. Inside the `<footer>`, create a [Bootstrap’s Input groups](https://getbootstrap.com/docs/4.5/components/input-group/#button-addons) of a text input and a button using 
    * give the group an id of `chatbar`
    * give the input field an id of `myMessage`
    * give the button an id of `sendButton`

    ```html
    <footer>
        <div id="chatbar" class="input-group mb-3">
            <input
                type="text"
                id="myMessage"
                class="form-control"
                placeholder="Type a message ...">
            <div class="input-group-append">
                <button
                    class="btn btn-outline-primary"
                    id="sendButton"
                    type="button">Send</button>
            </div>
        </div>
    </footer>
    ```
2. copy the following css code to your `styles.css` file

    ```css
    body,
    html {
        height: 100vh;
        overflow: hidden;
        margin: 0;
        padding: 0;
    }

    body {
        display: flex;
        flex-direction: column;
    }

    header,
        footer {
        background: #e9ecef;
    }

    .jumbotron {
        margin-bottom:0;
    }

    footer {
        padding: 0.5rem
    }

    #chat {
        flex: 1 0 auto;
        height: 0;
        overflow-y: auto;
        padding: 1rem;
    }
    ```

> The page should look like this.
<img alt="a page with a jumbotron and a chat box" src="assets/2.png" style="width:100%; border:1px #ddd solid;"/>

### Chat messages section
1. Inside of the `chat` div, copy the following ***(MOCK)*** messages.

```html
<div class="mine messages">
    <div class="message">
        Dude
    </div>
</div>
<div class="yours messages">
    <div class="message">
        Hey!
    </div>
    <div class="sender-info">
        Someone 2:59PM
    </div>
</div>

<div class="yours messages">
    <div class="message">
        You there?
    </div>
    <div class="sender-info">
        Someone else 3:00PM
    </div>
</div>

<div class="yours messages">
    <div class="message">
        Hello, how's it going? 😀
    </div>
    <div class="sender-info">
        Someone else2 3:02PM
    </div>
</div>

<div class="mine messages">
    <div class="message">
        Great thanks!
    </div>
</div>

<div class="mine messages">
    <div class="message">
        How about you?
    </div>
</div>
```
* You may paste the above multiple times to flood the chat div with messages and notice how you can scroll inside the chat section without the header or the input scrolling.
* Refresh the page, and you should see something like this.
<img alt="application with Chat messages" src="assets/3.png" style="width:100%; border:1px #ddd solid;"/>


### Styling the chat messages 👩‍🎨 🎨
1. Copy the following into the `styles.css` file
    ```css
    .sender-info {
        font-size: 10px;
        margin-top: -5px;
        color:grey;
    }

    .messages {
        display: flex;
        flex-direction: column;
    }

    .message {
        border-radius: 20px;
        padding: 8px 15px;
        margin-top: 5px;
        margin-bottom: 5px;
        display: inline-block;
    }

    .yours {
        align-items: flex-start;
    }

    .yours .message {
        margin-right: 25%;
        background-color: #eee;
        position: relative;
    }

    .yours .message:before {
        content: "";
        position: absolute;
        z-index: 0;
        bottom: 0;
        left: -7px;
        height: 20px;
        width: 20px;
        background: #eee;
        border-bottom-right-radius: 15px;
    }

    .yours .message:after {
        content: "";
        position: absolute;
        z-index: 1;
        bottom: 0;
        left: -10px;
        width: 10px;
        height: 20px;
        background: white;
        border-bottom-right-radius: 10px;
    }

    .mine {
        align-items: flex-end;
    }

    .mine .message {
        color: white;
        margin-left: 25%;
        background: linear-gradient(to bottom, #00D0EA 0%, #0085D1 100%);
        background-attachment: fixed;
        position: relative;
    }

    .mine .message:before {
        content: "";
        position: absolute;
        z-index: 0;
        bottom: 0;
        right: -8px;
        height: 20px;
        width: 20px;
        background: linear-gradient(to bottom, #00D0EA 0%, #0085D1 100%);
        background-attachment: fixed;
        border-bottom-left-radius: 15px;
    }

    .mine .message:after {
        content: "";
        position: absolute;
        z-index: 1;
        bottom: 0;
        right: -10px;
        width: 10px;
        height: 20px;
        background: white;
        border-bottom-left-radius: 10px;
    }
    ```

* Now refresh the page and **LOOK AT THAT** 🎉🎉🎉
<img alt="Styled chat messages" src="assets/4.png" style="width:100%; border:1px #ddd solid;"/>

**Now Enough HTML and CSS .. On to JavaScript**

## JavaScript Instructions (Bringing it to life)
**Workflow**

Before we start Building the application code, we need to fully imagine and visualize the process/workflow. 
* Getting messages:
    * Get/Query/Fetch all the messages from the server.
    * Parse and format the messages to present them on the screen.
    * Continiously Fetch the messages from the server to keep the messages up-to-date.
* Sending messages:
    * Get the user's name from the input field in the header.
    * Send the message in the format that the API is expecting.

### Getting Messages:
1. Create references to the HTML elements that we’ll need.
    * nameInput
    * messageInput
    * sendButton
    * chatBox

```js
const nameInput = document.getElementById("myName");
const myMessage = document.getElementById("myMessage");
const sendButton = document.getElementById("sendButton");
const chatBox = document.getElementById("chat");
```

2. Create an `updateMessagesInChatBox()` function. This function will:
    * fetch messages from server - `fetchMessages()`
    * loop over the recieved messages to convert them to `html` elements - `formatMessages()`
        * the function will mark the messages as (incoming/outgoing) or (yours/anyone else's) based on the sender name in the textbox.
    * Add the formatted messages to the chatbox. - `updateChatBox()`
        * OR more accuretly, clear and the chatbox and insert the newly formatted messages.

    ```js
    function updateMessages() {
        // Fetch Messages
        // Loop over the messages. Inside the loop we will
            // get each message
            // format it
            // add it to the chatbox
    }
    ```

4. Create a function that uses the FetchAPI to requests messages from the server.
    * URL to the Server is [https://it3049c-chat-application.herokuapp.com](https://it3049c-chat-application.herokuapp.com)
    * URL to the link to get the messages is [https://it3049c-chat-application.herokuapp.com/messages](https://it3049c-chat-application.herokuapp.com/messages)
    * sometime, the server might be idle and would take a few minutes to wake up again.

    ```js
    const serverURL = `https://it3049c-chat-application.herokuapp.com/messages`;

    function fetchMessages() {
        return fetch(serverURL)
            .then( response => response.json())
    }
    ```

5. Call `fetchMessages()` from `updateMessages()`
    * Notice, because `fetchMessages()` is an asyncronous function that returns a promise rather then the actual result, I had to make `updateMessages()` an `async` function as well and instruct it to await the results from `fetchMessages()`.

    ```js
    async function updateMessages() {
        // Fetch Messages
        const messages = await fetchMessages();

        // Loop over the messages. Inside the loop we will
            // get each message
            // format it
            // add it to the chatbox
    }
    ```
    * try to log the `messages` variable to the console to confirm the structure of each message looks like this

    ```json
    {
        "id": 1,
        "text": "This is my message",
        "timestamp": 1537410673072
    }
    ```

6. Create a formatter function that will take the `message` object and the username `myName` (from the text field) as parameters and return `HTML`.
    * the function will need to parse the timestamp to a readable format.
        * Obvi, `1537410673072` is not a readable format
    * compare the value of the `messages.sender` and the text input field, `myName`:
        * if it's the same, then use the class `mine` around the message div.
        * if it's not the same, use the class `yours` around the message div.

    ```js
    function formatMessage(message, myName) {
        const time = new Date(message.timestamp);
        const formattedTime = `${time.getHours()}:${time.getMinutes()}`;

        if (myName === message.sender) {
            return `
            <div class="mine messages">
                <div class="message">
                    ${message.text}
                </div>
                <div class="sender-info">
                    ${formattedTime}
                </div>
            </div>
            `
        } else {
            return `
                <div class="yours messages">
                    <div class="message">
                        ${message.text}
                    </div>
                    <div class="sender-info">
                        ${message.sender} ${formattedTime}
                    </div>
                </div>
            `
        }
    }
    ```

7. Now we loop over the array of the messages, format them and add them to the chatbox.

```js
async function updateMessages() {
    // Fetch Messages
    const messages = await fetchMessages();
    // Loop over the messages. Inside the loop we will:
        // get each message
        // format it
        // add it to the chatbox
    let formattedMessages = "";
    messages.forEach(message => {
        formattedMessages += formatMessage(message, nameInput.value);
    });
    chatBox.innerHTML = formattedMessages;
}
```
8. We need to make sure the function is called.
    * otherwise, we won't see any difference.

```js
updateMessages()
```

9. Use `setInterval()` to call this function once every 10 seconds to keep the new messages coming.

    ```js
    setInterval(updateMessages, 10000);
    ```
    * the number `10000` in this scenario is what we refer to as a magic number. it's a value of some significance but someone looking at this may not easily understand what this value is
        * we like to set this value to a variable to make this a bit more readable.
    ```js
    const MILLISECONDS_IN_TEN_SECONDS = 10000;
    setInterval(updateMessages, MILLISECONDS_IN_TEN_SECONDS);
    ```

### Sending Messages
1. Create a send function that would:
    * take the username, and message text as parameter
    * construct a json object with the following properties `sender`, `text`, and `timestamp`
    * send messages to the server here

**Using FetchAPI**
```js
const serverURL = `https://it3049c-chat-application.herokuapp.com/messages`; // This has been declared before
...
function sendMessages (username, text) {
    const newMessage = {
        sender: username,
        text: text,
        timestamp: new Date()
    }

fetch(serverURL, {
        method: `POST`,
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(newMessage)
    });
}
```
**OR Using JQuery**
```js
function sendMessages (username, text) {
    const newMessage = {
        sender: username,
        text: text,
        timestamp: new Date()
    }

    $.post(serverURL, newMessage);
}
```

2. create an Event Listener to listen to the `click` event on the send button. This event handler will:
    * send the message to the server and clear the text field to prepare for a new message to be sent
    * clear the message text field

```js
sendButton.addEventListener("click", function(sendButtonClickEvent) {
    sendButtonClickEvent.preventDefault();
    const sender = nameInput.value;
    const message = myMessage.value;

    sendMessages(sender,message);
    myMessage.value = "";
});
```



## Hosting and Submission
### GitHub Pages
1. Follow the following [instructions](https://help.github.com/en/enterprise/2.13/user/articles/configuring-a-publishing-source-for-github-pages#enabling-github-pages-to-publish-your-site-from-master-or-gh-pages) to setup github pages and **publish your page from `master`**.

### Submission
1. update the `README.md` file with your self-grading and self-reflection.

2. On Canvas, submit the repository link and the hosted github pages link.

# Extra Credit
* Create a refresh button to refresh the messages sooner than the 10 seconds auto-update.
* use the colorAPI to change the color scheme of the application.
* Invisitigate and implement a mechanism to save data in the browser (even after you close the browser and open it again, try to do that.)
