<!--
Market: SF
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# HTML Forms

## Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

Forms are an important way a web application receive user input. The proper use of forms makes it easier to develop accessible websites with a good user experience.

## What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

- Understand the basics of the client/server model
- Evaluate the proper usage of HTML form and input options
- Compare and contrast the difference between a `method` and an `action`
- Create forms that generate query parameters

## Where should we be now?
<!-- call out the skills that are prerequisites -->
*Before this workshop, developers should already be able to:*

- Write HTML & JavaScript
- Understand the basics of the client/server model

### What is HTTP?

![image](https://cloud.githubusercontent.com/assets/6520345/20934822/5eab66aa-bb91-11e6-937b-ffe856952f1a.png)


HTTP stands for *hypertext transfer protocol*. It is the standard that determines the data format of any information moving between websites. To make an HTTP request, you need three things.

1. An address where you'll make the request.
2. An HTTP verb, which will specify the action you request at that address. Here are the possible HTTP verbs:

    * POST - (Create) create an entry in the database we access.
    * GET - (Read) find and return an entry from the database.
    * PUT - (Update/replace) change a specific entry at that address by replacing it with a new entry.
    * PATCH - (Update/modify) change a specific entry at that address by updating it with new data.
    * DELETE - (Delete) remove an entry from the database.

3. (Optional) Any data that might be necessary in passing along your request.

**Client / Server Model**

![client/server](https://mdn.mozillademos.org/files/4291/client-server.png)


### An Example `<form>` Element (Tag)

```html
<form method="POST" action="/entries">
  <input type="text" name="title" />
  <input type="text" name="content" />
  <input type="submit" value="Create an Entry" />
</form>
```

#### Attributes

By default, when a form is submitted, it generates an HTTP request. In the opening of the `<form>` tag you can see two attributes: `method` & `action`

- **method**: the HTTP verb (method) that the browser uses to submit the form.
- **action**: the path of the HTTP request page that processes the information submitted via the form. Although it's a bit strange, `action` specifies *where* to take action - it's the address for the HTTP request.

>A `route` is simply a combination of a method & action. For example `GET '/page'` or `POST '/users'` are both valid routes.

>For now simply understand that it is convention for [GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) to be used in a request when the person using your site (the client) wants to receive data, and for [POST](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.5) to be used in a request when the client wants to send data.

### Challenge: Doomed?

Create an html `form` that, on submit, sends the user to "havewedestroyedtheworldyet.com". This form will only have one input: the submit button. Hint: what's the form action? Bonus: Can you change the submit button to say "Are we doomed?".

<details>
<summary>Example solution</summary>

```html
<form action="http://havewedestroyedtheworldyet.com" method="GET">
  <input type="submit" value="Are we doomed!?">
</form>
```

</details>



## Common Inputs

| Field Type | HTML Code | Widget (Control) | Notes |
|:-- |:-- |:-- |:-- |
| plain text | `<input type="text">` | ![<input type="text">][text] | the type attribute can be omitted |
| password field | `<input type="password">` | ![<input type="password">][text] | echoes dots instead of characters |
| text area | `<textarea></textarea>` | ![<textarea></textarea>][area] | a more customizable plain text area |
| checkbox | `<input type="checkbox">` | ![<input type="checkbox">][check] | can be toggled on or off |
| radio button | `<input type="radio">` | ![<input type="radio" name="group"> <input type="radio" name="group">][radio] | can be grouped with other inputs |
| drop-down lists | `<select><option>` | ![<select><option>Option 1</option><option>Option 2</option></select>][select] | [check here for more info](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) |
| file picker | `<input type="file">` | ![<input type="file">][file] | pops up an “open file” dialog |
| hidden field | `<input type="hidden">` |  | nothing there!
| submit button | `<input type="submit">` | ![<input type="submit">][submit] | activates the form's submission <br/>(a `POST` request or <br/>Javascript action) |

<!-- Images -->
[text]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-text.png
[area]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/textarea.png
[check]:  https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-checkbox.png
[radio]:  https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-radio.png
[select]: https://raw.github.com/h4w5/html_form_cheatsheet_images/master/select-option.png
[file]:   https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-file.png
[submit]: https://raw.github.com/h4w5/html_form_cheatsheet_images/master/input-submit.png

### Important Attributes

All input types (including `<textarea>`s) can have the following attributes:

- **`type`**: the type of data that is being input (affects the "widget" that is used to display this element by the browser).
- **`name`**: the key used to describe this data in the HTTP request.
- **`id`**: the unique identifier that other HTML elements, JavaScript and CSS use to access this
  element in the browser.
- **`value`**: the default data that is assigned to the element.
- **`placeholder`**: not a default value, but a useful HTML5 addition of a data "prompt" for an input.
- **`autofocus`**: defaults the cursor to a specific input when the page originally loads. You can only have one autofocus on your page.
- **`disabled`**: a Boolean attribute indicating that the "widget" is not available for interaction.
- **`required`**: a Boolean attribute indicating that the field must have a value / cannot be left empty.

Radio buttons or checkboxes:

- **`checked`**: a Boolean that indicates whether the control is selected by default (is false unless).
- **`name`**: the group to which this element is connected. For radio buttons, only one element per group (or name) can be checked.
- **`value`**: the data or value that is returned for a specific group (a multi-element control), if this element is checked.


You may be thinking to yourself, "an HTTP request has optional data that it should be able to send too. Where does that come from in the form?"

Great question!

The data portion comes from the `name` and `value` attributes of the inputs!

### Challenge: Login Form

Create an html `form` with two inputs: one for a username (named "username"), the other for password (named "password") (normally you don't see your password when you type it, so make sure it's blocked out!). What happens in the URL when you click submit?

<details>
<summary>Example solution</summary>

```html
<form>
	<input type="text" name="username" placeholder=" username..." required>
	<input type="password" password="password" placeholder="password..." required>
	<input type="submit">
</form>
```

</details>


## Form Submission Experiments

**1)** Given the following HTML...

``` html
<form>
    <input name="instrument" value="bongos"> <!-- Text Field -->
    <input type="submit">                   <!-- Submit Button -->
</form>
```

<details>
<summary> <strong>What endpoint/action are we submitting to?</strong> </summary>
<br>
We did not supply a form `action`. That means that it will default to the current endpoint. In otherwords, you will refresh the current page.
</details>

<details>
<summary><strong>What data will be submitted to the server?</strong></summary>
<br>
instrument: "bongos"
</details>

<details>
<summary><strong>What will that data look like? How will it be formatted</strong></summary>
<br>
`?instrument=bongos`
</details>


**2)** Given the following HTML...

``` html
<form id="artist-search-form" action="https://musicbrainz.org/search" method="GET">
    <label for="query">Search by Artist</label>
    <input id="query" name="query" value="Adele">
    <input id="type" name="type" value="artist" hidden>
    <input type="submit">
</form>
```

<details>
<summary><strong>What endpoint/action are we submitting to?</strong></summary>
<br>
We are making a "GET" request to "https://musicbrainz.org/search".
</details>

<details>
<summary><strong>What data will be submitted to the server?</strong></summary>
<br>
query: "Adele", type: "artist"
</details>

<details>
<summary><strong>What will that data look like? How will it be formatted?</strong></summary>
<br>
It will be in the form of a query parameter: `?query=adele&type=artist`
</details>

## Form Submission

Sometimes we want to submit a form, in the background, without ever refreshing the page. This is a common pattern in modern "single page applications". How do you submit form data *in the background*?

When a form is submitted it triggers the `submit` event. We can set an event listener on the form using an element's method [`.addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener). Additionally, in order to **stop** the form from submitting, we have to prevent its *default* behavior. Calling `preventDefault` will allow us to later use AJAX to submit the form data without refreshing the page!

``` javascript
$("#artist-search-form").addEventListener("submit", function(event) {
    event.preventDefault(); // Stops the form from submitting!
    alert("We've submitted the form!")
})
```

>Why is `.preventDefault` useful?

Let's grab data from the form by using the keyword `this`, which refers to the element that triggered the event — aka, the form! Then let's drill down into the forms data using `.querySelector` to target children elements inside it.

``` javascript
// target the form
var artistSearchFrom = document.querySelector("#artist-search-form");
artistSearchFrom.addEventListener("submit", function(event) {
  // stop the form from submitting!
  event.preventDefault();
  // grab the user input
  var artist = this.querySelector("#query").value;
  var type = this.querySelector("#type").value;
  // do something with the user input
  console.log(artist, "is a", type);
});
```

## The `<label>` element and `placeholder` attribute

We encourage you to always use the optional `<label>` tag with each of your form inputs.

>"This is the most important element if you want to build accessible forms." — MDN

**Label**

```html
<label for="password">Password:</label>
<input id="password" type="text" name="password" />
```

>"*Do not use the placeholder attribute instead of a <label> element*. Their purposes are different: the <label> attribute describes the role of the form element; that is, it indicates what kind of information is expected, the placeholder attribute is a hint about the format the content should take. There are cases in which the placeholder attribute is never displayed to the user, so the form must be understandable without it." -MDN


**Placeholder**

```html
<input type="text" name="username" placeholder="Enter a unique username...">
```

> Make sure a label's `for` attribute matches the input's `id` attribute!

## Common Validations

Form validations help to prevent users from submitting bad data to the server. They are very important to improve UX, but *do not increase the security* of the application. Examples of common validations:

* a missing or empty field (required)
* an email address that was missing an "@" symbol (wrong pattern)
* a password that is obviously too short (invalid length)

#### `required` attribute

Try submitting the below form without entering your name:

```html
<form>
  <label for="colorField">What is your favorite color?</label>
  <input id="colorField" name="favColor" required>
  <button>Submit</button>
</form>
```

Notice the `required` attribute on the input. Therefore, the form will not submit until some information is entered into the field.

#### `pattern` attribute

```html
<form>
  <label for="kindOfBob">Do you go by bob or bobert?</label>
  <input id="kindOfBob" name="bobType" pattern="bob|bobert" required>
  <button>Submit</button>
</form>
```

The `pattern` attribute allows us to specify the values we will accept. In this case only `bob` or `bobert` are acceptable.

#### `length` attribute

You may need the user to enter a specific amount of characters. Let's say you need a username to be at least 6 characters. You can use the `minlength` or `maxlength` attributes to help.

```html
<form>
  <label for="password">What's your password?</label>
  <input id="password" type="password" name="password" minlength="8" required>
  <button>Submit</button>
</form>
```

## Independent Practice

**1)** Create an html form that contains the html5 [color-picker](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/color) input (named "i"). When the user picks a color, let's say one with the hex code `#18967A`, and clicks submit, redirect them to, e.g. "https://www.wolframalpha.com/input/?i=%2318967A".

> **Note:** the `#` character automatically gets converted to `%23` in this context because it is a special character and **not a fragment** in this context.

<details>
<summary>Example solution</summary>

```html
<form action="https://www.wolframalpha.com/input/" method="GET">
  <input type="color" name="i">
  <input type="submit" value="search">
</form>
```

</details>

**2)** Create an html form that searches github for code examples that match a specific query (q) and language (l). Use `html`, `javascript`, and `ruby` as the languages the user can select from a drop down menu. A search for "audio" in the language "javascript" should direct to https://github.com/search?q=audio&l=javascript.

<details>
<summary>Example solution</summary>

```html
<form action="https://github.com/search" method="GET">
  <input type="text" name="q" placeholder="search">
  <select name="l">
    <option value="HTML">HTML</option>
    <option value="Javascript">Javascript</option>
    <option value="Ruby">Ruby</option>
  </select>
  <input type="submit" value="Search Github">
</form>
```

</details>

**3)** Create an HTML form with at least 4 different input types. Make it appear in 2 columns on a large screen and 1 column on a mobile screen. Don't include an `action` or `method` attribute. Instead, create an event listener that prevents the default action from happening and instead `console.log`s all of the names and values from the form. (Hint: investigate [`serialize`](https://api.jquery.com/serialize/) to help you gather these names and values.)

## Closing Thoughts

* What is a form `method` and a form `action`?
* How do we prevent a form's submission from leaving or refreshing the current page?
* Do validations make our application more secure?

## Additional Resources

MDN has a number of exhaustive resources on HTML forms and inputs. It can be a lot to absorb, so look for patterns and try to grasp the big picture.

* [HTML Form Reference](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms)
* [HTML Input Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
* [Native Form Widgets](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/The_native_form_widgets)
* [Form Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Data_form_validation)
* [Inspiration for Text Inputs](http://tympanus.net/codrops/2015/01/08/inspiration-text-input-effects/)
