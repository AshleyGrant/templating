---
{
  "name": "Templating: Custom Elements Basics",
  "culture": "en-US",
  "description": "An overview of the Aurelia templating engine's custom element functionality basics. Custom Elements are used to add custom components to Aurelia applications.",
  "engines" : { "aurelia-doc" : "^1.0.0" },
  "author": {
  	"name": "Ashley Grant",
  	"url": "http://www.ashleygrant.com"
  },
  "contributors": [],
  "translators": [],
  "keywords": ["JavaScript", "Templating", "Custom Elements", "Basics"]
}
---
## [Introduction](aurelia-doc://section/1/version/1.0.0)

Custom elements are the primary tool an Aurelia application developer will utilize for componentizing an application.

## [HTML Only Custom Element](aurelia-doc://section/2/version/1.0.0)

The simplest way to create an Aurelia custom element is to create an Aurelia view template in an HTML file and then require it in to another Aurelia view template. HTML only custom elements are a highly useful strategy for dealing with functionality that has no need for ViewModel logic but is likely to be reused. The element name will be the same as the HTML file name, without the extension. When requiring an HTML only custom element in to a view, you must include the `.html` extension.  It is even possible to create bindable properties for an HTML only custom element by putting a comma separated list of property names on the `bindable` attribute of the `template` element. The Aurelia convention of converting camelCase bindable properties to dash-case applies to properties provided to the `bindable` attribute, as shown in the following example.

<code-listing heading="hello-world.html">
  <source-code lang="HTML">
    <template bindable="firstName, lastName">
      Hello, ${firstName} ${lastName}!
    </template>
  </source-code>
</code-listing>

<code-listing heading="app.html">
  <source-code lang="HTML">
    <template>
      <require from="./hello-world.html"></require>

      <hello-world first-name="Albert" last-name="Einstein"></hello-world>
    </template>
  </source-code>
</code-listing>

HTML only custom elements may require in other custom elements and attributes as well as utilizing any other view resource just like any other Aurelia component may. HTML only custom elements also support explicit two-way databinding for properties, though it is not possible to create properties that default to two-way databinding with HTML only custom elements. For that type of functionality, you will need to provide a ViewModel for your custom element.

The following example shows an Aurelia view utilzing two-way databinding to an example HTML only custom element. The example HTML only custom element itself requires in other custom elements, and utilizes two-way databinding to those custom elements. Note that it is possible to use the full power of Aurelia's templating engine from an HTML custom element, such as using the `debounce` binding behavior.

<code-listing heading="app.html">
  <source-code lang="HTML">
    <template>
      <require from="./example.html"></require>

      Hello, ${guest}!
      <example name.two-way="guest"></example>
    </template>
  </source-code>
</code-listing>

<code-listing heading="example.html">
  <source-code lang="HTML">
    <template bindable="name">
      <require from="./yes-or-no.html"></require>
      <require from="./say-goodbye.html"></require>

      <p>What is your name? <input type="text" value.bind="name & debounce" /></p>
      <yes-or-no question="Are you leaving?" answer.two-way="sayGoodbye"></yes-or-no>
      <say-goodbye if.bind="sayGoodbye" name.bind="name"></say-goodbye>
    </template>
  </source-code>
</code-listing>

<code-listing heading="yes-or-no.html">
  <source-code lang="HTML">
    <template bindable="question, answer">
      <p>
        ${question} <input type="checkbox" checked.bind="answer" />
      </p>
    </template>
  </source-code>
</code-listing>

<code-listing heading="say-goodbye.html">
  <source-code lang="HTML">
    <template bindable="name">
      Goodbye, ${name}!
    </template>
  </source-code>
</code-listing>

## [Standard Custom Element Conventions](aurelia-doc://section/3/version/1.0.0)

 Creating custom elements using Aurelia is extremely simple. Simply creating a JavaScript and HTML file pair with the same name is all that is necessary to create an Aurelia custom element. The HTML file must contain an Aurelia template wrapped in a `template` element. The JavaScript file must export a JavaScript class
