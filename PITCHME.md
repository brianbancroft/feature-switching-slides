## Feature Switching

#### Explanation and Execution of Feature Switching

---

## Overview!


@fa[question gp-tip] Lecture 1: What is switching and how will it be used?
- (20 minutes) |

@fa[flag-checkered gp-tip] Lecture 2: Implementing it on the front-end
- (30 minutes) |

@fa[battery-half gp-tip] Lecture 3: Implementing it on the back-end
- (15 minutes) |


---

### Lesson 1: Explanation and Usage

- What: Allows us to deploy partial or fresh features to production without being exposed to users |
- Where: Anytime you'll build a new feature |
- Why: To reduce the amount of time it takes to build and approve new features. |

---
### What is feature switching

---
### What is feature switching

```test
  Feature switching is something which
  allows us to change behaviour without changing code.
```

---
### What is feature switching

---
### What is feature switching

#### Characteristics

- Controlled by the Database |
- Allows cut off at the feature level |
- Allows features to be disabled by user groups |

---
### The Process


---

First, build a new feature. Ask the following:

- Does it require a route? |
- Is it a component or entire feature set? |
- Is it just an action? |

---

Second, pick a name. For a feature set:

- hub_ui_featureset_name
```ruby
''
```

---

Second, pick a name. For a feature set:

- hub_ui_featureset_name
```ruby
`hub_ui_users_lookup`
```

---
For a feature set action:

- _jsm_ui_featureset_name_action_name`
```ruby
''
```

---
For a feature set action:

- _jsm_ui_featureset_name_action_name`
```ruby
`jsm_ui_resumes_make_primary`
```

---

Third, enter it in the Database using the _Rails Console_
```ruby
$ rails c
> Flipper.enable('jsm_ui_resumes_make_primary')
```
@[1-3](Always use *snake_case* when creating the switch in the DB.)


---

If it is a component or action, restrict it at the template level
```hbs
{{#if features.jsmUiResumesMakePrimary}}
  {{cards/primary-resume-card}}
{{/if}}
```
@[1-3](While it is snake-case in the Database, It will appear as *camelCase* in the Ember apps.)


---
### The Process

---

If it is a separate view, restrict it in the following places:

- At the route level (js)
- At the menu item level (template/hbs)

---

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
    {{#link-to 'users.index' class="..."
    data-test-users-sidenav="..."}}
      <div class="icon-tooltip"
        data-toggle="tooltip"
        data-placement="right"
        title="User Lookup"
        data-container="body">
      </div>
      <i class="icon icon-search"></i>
      <span class="nav__title">User Lookup</span>
    {{/link-to}}
  </li>
{{/if}}

```
---

### Review

- What is feature switching
- How is it employed

---?image=assets/image/gitpitch-audience.jpg

### Questions?

<br>

@fa[twitter gp-contact](@brian_bancroft)

@fa[medium gp-contact](@brian_bancroft)

@fa[github gp-contact](brianbancroft)

