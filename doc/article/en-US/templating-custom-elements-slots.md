---
{
  "name": "Templating: Custom Elements - Content and Slots",
  "culture": "en-US",
  "description": "An overview of the Aurelia templating engine's custom element slot and content functionality.",
  "engines" : { "aurelia-doc" : "^1.0.0" },
  "author": {
  	"name": "Ashley Grant",
  	"url": "http://www.ashleygrant.com"
  },
  "contributors": [],
  "translators": [],
  "keywords": ["JavaScript", "Templating", "Custom Elements", "Content", "Slot"]
}
---

## [Custom Elements with Content](aurelia-doc://section/5/version/1.0.0)

Up until now, we have created custom elements that are empty when used in a view. But what if we wanted to create a custom element that could have content inside it. That content could be text or even other HTML. To access this content, we can use the `content` element in the view for our custom element. There is one "gotcha" when using the `content` element: it must be used 'statically,' and cannot be dynamically added or removed from the DOM (for example by using `<content if.bind=...`). If you wish to dynamically show or hide the `content`, consider using Aurelia's `show.bind` behavior.

Let's look at a simple example of using `content`. We'll create a `name-tag` custom element that supports using having the name as its content.

<code-listing heading="secret-message.html">
  <source-code lang="HTML">
    <template>
      <h3>HELLO</h3>
      <h4>my name is</h4>
      <div class="name">
        <content></content>
      </div>
    </template>
  </source-code>
</code-listing>

<code-listing heading="app.html">
  <source-code lang="HTML">
    <template>
      <require from="./name-tag.html"></require>

      <name-tag>Ralphie</name-tag>
    </template>
  </source-code>
</code-listing>

When this custom element is rendered, "Ralphie" will be inserted where the `content` element is in the template. The `content` element can only be used once in a custom element's view.

