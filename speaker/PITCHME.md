## Feature Switching

### Explanation and Execution of Feature Switching

---

## Overview!


@fa[question gp-tip] Lecture 1: What is switching and how will it be used? (20 minutes)

@fa[flag-checkered gp-tip] Lecture 2: Implementing it on the front-end (30 minutes)

@fa[drivers-license-o gp-tip] Lecture 3: Implementing it on the back-end (20 minutes)


---

<p><span class="slide-title">Lesson 1: Explanation and Usage</span></p>



Note:
In the next 20 minutes, I will give an overview on what feature switching is, and how we will be using it if it is green-lighted in the organization


---
<p><span class="slide-title">Lesson 1: Explanation and Usage</span></p>
- _What_: Allows us to deploy partial or fresh features to production without being exposed to users

---
<p><span class="slide-title">Lesson 1: Explanation and Usage</span></p>

- _What_: Allows us to deploy partial or fresh features to production without being exposed to users
- _Where_: Anytime you'll build a new feature

---
<p><span class="slide-title">Lesson 1: Explanation and Usage</span></p>


- _What_: Allows us to deploy partial or fresh features to production without being exposed to users
- _Where_: Anytime you'll build a new feature
- _Why_: To reduce the amount of time it takes to build and approve new features.

---
<p><span class="slide-title">What is feature switching</span></p>


#### A Definition
```
  Feature switching is something that allows us to change behaviour without changing code.
```

---
<p><span class="slide-title">What is Feature Switching</span></p>


#### Characteristics

- Controlled by the Database
- Allows cut off at the feature level
- Allows features to be disabled by user groups

---
<p><span class="slide-title">The Process</span></p>


---
<p><span class="slide-title">The Process</span></p>

First, build a new feature. Ask the following:

- Does it require a route
- Is it a component or entire feature set?
- Is it just an action?

---
<p><span class="slide-title">The Process</span></p>

Second, pick a name.

- `hub_ui_featureset_name`
- `hub_ui_users_lookup`
- `jsm_ui_resumes_make_primary`

---
<p><span class="slide-title">The Process</span></p>

Third, enter it in the Database using the _Rails Console_
```ruby
  $ rails c
  > Flipper.enable('jsm_ui_resumes_make_primary')
```
@[1-3](Always use *snake_case* when creating the switch in the DB.)


---
<p><span class="slide-title">The Process</span></p>

If it is a component or action, restrict it at the template level
```hbs
  {{#if features.jsmUiResumesMakePrimary}}
    {{cards/primary-resume-card}}
  {{/if}}
```
@[1-3](While it is snake-case in the Database, It will appear as *camelCase* in the Ember apps.)


---
<p><span class="slide-title">The Process</span></p>

If it is a separate view, restrict it in the following places:

- At the route level (js)
- At the menu item level (template/hbs)

---
<p><span class="slide-title">The Process</span></p>

At the _Route_ level:

```js
  beforeModel (transition) {
    this.get('can').checkFeature('hubUiUsersLookup', transition);
  },
```

---

At the _Template_ level

```hbs
  {{#if features.hubUiUsersLookup}}
    <li>
      {{#link-to 'users.index' class="side-menu__link"
      data-test-users-sidenav="data-test-users-sidenav"}}
        <div class="icon-tooltip"
          data-toggle="tooltip"
          data-placement="right"
          title="User Lookup"
          data-container="body">
        </div>
        <i class="icon icon-search" aria-hidden="true"></i>
        <span class="nav__title">User Lookup</span>
      {{/link-to}}
    </li>
  {{/if}}

```
---



## Template Features

- Code Presenting |
- Repo Source, Static Blocks, GIST |
- Custom CSS Styling |
- Slideshow Background Image |
- Slide-specific Background Images |
- Custom Logo, TOC, and Footnotes |

Note:
Keep yourself on track using lists within your speaker notes:

- Key insight.
- Supporting use case.
- Time to delve deeper.

---?code=src/go/server.go&lang=golang&title=Golang File

@[1,3-6](Present code found within any repo source file.)
@[8-18](Without ever leaving your slideshow.)
@[19-28](Using GitPitch code-presenting with (optional) annotations.)

Note:
Best to keep it simple. Try highlighting just one key message per slide.

---

@title[JavaScript Block]

<p><span class="slide-title">JavaScript Block</span></p>

```javascript
// Include http module.
var http = require("http");

// Create the server. Function passed as parameter
// is called on every request made.
http.createServer(function (request, response) {
  // Attach listener on end event.  This event is
  // called when client sent, awaiting response.
  request.on("end", function () {
    // Write headers to the response.
    // HTTP 200 status, Content-Type text/plain.
    response.writeHead(200, {
      'Content-Type': 'text/plain'
    });
    // Send data and end response.
    response.end('Hello HTTP!');
  });

// Listen on the 8080 port.
}).listen(8080);
```

@[1,2](You can present code inlined within your slide markdown too.)
@[9-17](Displayed using code-syntax highlighting just like your IDE.)
@[19-20](Again, all of this without ever leaving your slideshow.)

Note:
Perhaps it's time for an insightful anecdote to keep your
audience engaged?

---?gist=onetapbeyond/494e0fecaf0d6a2aa2acadfb8eb9d6e8&lang=scala&title=Scala GIST

@[23](You can even present code found within any GitHub GIST.)
@[41-53](GIST source code is beautifully rendered on any slide.)
@[57-62](And code-presenting works seamlessly for GIST too, both online and offline.)

Note:

Reinforce key points to drive home your message.

---

## Template Help

- [Code Presenting](https://github.com/gitpitch/gitpitch/wiki/Code-Presenting)
  + [Repo Source](https://github.com/gitpitch/gitpitch/wiki/Code-Delimiter-Slides), [Static Blocks](https://github.com/gitpitch/gitpitch/wiki/Code-Slides), [GIST](https://github.com/gitpitch/gitpitch/wiki/GIST-Slides)
- [Custom CSS Styling](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Custom-CSS)
- [Slideshow Background Image](https://github.com/gitpitch/gitpitch/wiki/Background-Setting)
- [Slide-specific Background Images](https://github.com/gitpitch/gitpitch/wiki/Image-Slides#background)
- [Custom Logo](https://github.com/gitpitch/gitpitch/wiki/Logo-Setting), [TOC](https://github.com/gitpitch/gitpitch/wiki/Table-of-Contents), and [Footnotes](https://github.com/gitpitch/gitpitch/wiki/Footnote-Setting)

Note:

Let your audience know where they can find additional
help.

And where they can find your presentaton slides,
online @ [GitPitch.com](https://gitpitch.com) :)

---

### Template Versions

- #### [Base Template  @fa[external-link gp-download]](https://gitpitch.com/gitpitch/templates/netflix)
- #### [Code Maximized @fa[external-link gp-download]](https://gitpitch.com/gitpitch/templates/netflix?p=codemax)
- #### [Speaker Notes @fa[external-link gp-download]](https://gitpitch.com/gitpitch/templates/netflix?p=speaker)

Note:

You can use the links on this slide to explore alternate
versions of this template.

---

### Questions?

<br>

@fa[twitter gp-contact](@brian_bancroft)

@fa[github gp-contact](brianbancroft)

@fa[medium gp-contact](@brian_bancroft)

Note:

Encourage questions, it's a great opportunity to
learn from your audience.

---?image=assets/image/gitpitch-audience.jpg

@title[Download this Template!]

### Get your presentation started!
### [Download this template @fa[external-link gp-download]](https://gitpitch.com/template/download/netflix)

Note:

Now it's your turn. The fastest way from idea to presentation
is to download a GitPitch presentation template. Visit the
Template Gallery [here](https://gitpitch.com/templates.html).

