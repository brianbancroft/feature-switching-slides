# Feature Switching Presentation

Presentation on how to do feature switcing. Full slidedeck at PITCHME.md

## EXERCISE CONTENT FOR PART 2

The following is the end content for the skill-section of the lecture.

### Restriction labels in demo

| Camel | Snake |
| ----- | ----- |
| hubUiSpecialButton | `hub_ui_special_button` |
| hubUiSpecialButtonClear | `hub_ui_special_button_clear` |
| hubUiOffices | `hub_ui_offices` |


### Special Data Components

#### Component
Location: `components/cards/special-button-card.hbs`
```hbs
<div class="row">
  <div class="col-md-3" style="border-right: 1px solid #333;">
    {{!-- For items that deliberately require a call to the backend --}}
    {{#if features.hubUiSpecialButton}}
      <button class="btn btn-primary" {{action "buttonPress"}}>New Quote</button>
    {{/if}}
    {{!-- Example of limiting features at the action level --}}
    {{#if features.hubUiSpecialButtonClear}}
      <button class="btn btn-danger" {{action "clearMessage"}} style="margin-top: 10px;">Clear</button>
    {{/if}}
  </div>
  <div class="col-md-9">
    {{message}}
  </div>
</div>
```

#### Route-level restriction
Location: `route/offices/index.js`

```js
beforeModel(transition) {
  this.get('can').checkRouteFeature('features.hubUiOffices');
  this.get('can').checkRoute('editOffices', transition);
},
```
