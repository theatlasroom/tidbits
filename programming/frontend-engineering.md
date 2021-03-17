# Frontend Engineering

- [Template](https://docs.google.com/presentation/d/124zFVyJXes8XuVViceHw4ZhS6eFCNt1RlBZ3V54viME/edit#slide=id.gb0764ef3d4_0_15)

## Overview

- About me 👋

- What is Frontend Engineering

  - History + Why
  - Understanding users + understanding the business
  - Types of FE?

- Overview of role + skills

  - Collaboration + communication (the secret sauce)
  - Application architecture
    - Async communication / events
    - Data fetching
    - Managing application state
    - SPAs
  - Responsive web design

- Key tools and technologies

  - HTML + CSS + JS
  - Frameworks and libraries
  - Build tools / Bundlers / Task Runners

- Common challenges

  - Performance
  - Framework / language churn
  - Reliability and safety
    - JS time / date / number rounding pain

- Emerging trends

## Introduction

## What + Why

### What is frontend engineering

- Frontend usually refers to the presentation layer of some kind of software or hardware device
  - A layer of abstraction to simplify how a user interacts with a complex system
- In the context of web development the client is typically a web browser
- So we can think of it as a discipline within web development that (mostly) deals with what happens on the client side of a web site or application
- The responsibilities of this role are usually to ensure development a user interface that is used to interact with a system, product or service

### Why do we need FE?

- The internet has become an integral part of the lives of many people around the world
- Bridging the gap between users and a product or service, informed
  by design decisions

### Understanding users + understanding the business

- Understanding users
  - User demand, web design has improved dramatically over the years, so users have much higher expectations of how web applications should look, feel and operate
  - It should "just work"
  - Catering for the various conditions in which users use web applications, on their phone on a busy train vs in an office with dual 4K monitors
- Understanding the companys goals and business process, these are often exposed via APIs or databases
  - knowing how to connect these services to the

### Typical types of FE?

- UI focused
- Application focused
- Frontend architect

<details>
<summary>Notes</summary>
In a typically medium to large development team, it is likely there will be frontend engineers that work across various different aspects.

Depending on the company / team size / stage of the product some roles will focus more one area over the others, but generally these are all the types of roles frontend engineers will typically be expected to be able to work across.

Across any of these types of roles, a solid understanding of HTML, CSS and Javascript is vital to be able to work effectively.

</details>

#### UI focused

> Image of storybook + CSS + JS + HTML

<details>
<summary>Notes</summary>
Some frontend engineer roles e are more focused on the user side, this might require tasks such as development of reuseable components like buttons, form fields and layouts that adhere to the branding and style guidelines for the company.

Often in these kind of scenarios, the engineers will work closely with UX researchers and designers to develop components. These components provide an important framework for other engineers to quickly prototype and build new interfaces, without having to worry if the interfaces they are building are consistent with other parts of the website or application.

Some other key responsibilities might include ensure adhereance to web accessibility guidelines, as well as making sure the code behind the components is semantic and well structured.

</details>

#### Application focused

> Image of a UI + graphql + REST + AJAX

<details>
<summary>Notes</summary
Other frontend engineers focus on the application layer, this usually entails building out user interfaces, connecting to backend APIs or other data sources, performing transformations or calculations on the frontend to prepare data for display and implementing features.

Often these engineers will make use of the common, or shared components that have been developed, composing them togethor on the screen to complete a specific feature, while also working closely with backend engineers to ensure the relevant API endpoints and data is available for the features to work correctly, this is closer to the kind of role I perform at gitlab.

</details>

#### Frontend Architect

> Image of a webpack + eslint + prettier + nodejs

<details>
<summary>Notes</summary>
While not a strictly separate role, there is often a need in any medium to large team to have frontend engineers focused on tooling and infrastructure to help other engineers efficiently and effectively build features or components.

This can often involve a wide range of tasks such as implementing linters to ensure the codebase largely adheres to common standards and automate some of this process, it can also involve building out templates or starters to easily allow new applications to be developed, polyfilling features that might not be supported in all browsers and it can also include configuring build systems to bundle, minify and split all the code to reduce the size of code that is shipped to the user.

While these tasks do not directly impact the user, they can help ensure the development team is able to ship features, consistently and efficiently.

</details>

## Overview of role + skills

### Collaboration + communication (the secret sauce)

- Often overlooked as a key skill
- Most Frontend roles will require some collaboration with UX / designers + backend engineers
- The ability to understand requirements and effectively articulate constraints will always help avoid misunderstandings

<details>
<summary>Notes</summary>
- Overarching goals
  - Ensures that users are able to complete goals with a product
  - Ensures that the product adheres to the companys vision, brand and design philosophies
- In a typical cross functional team (design + FE + BE)
  - Designers will develop prototypes for a user flow, detailing a process / service / product that has been designed based on the needs of a user
  - BE implement the business logic to execute the tasks (interacting with a databse, sending email notifications, retrieving the latest readings from the Hubble telescope)
  - FE are there to glue these things togethor on the screen, ensuring the end result is consistent, performs well and is robust enough to withstanding changing conditions (internet disconnects, server crashes and stops responding)
- To achieve these goals, FEs require knowledge of:
  - The goals of the user, what should this interface enable a user to achieve?
  - ~~Boundaries of their chosen tools, current architecture (if there is one), or the design system~~
  - Boundaries of the BE services and processes, what are the edge cases? How much data do we get? How often is the data refreshed
  - The existing application architecture (if there is one)
- This requires lots of communication and collaboration with other disciplines to ensure the end result works as expected, or the correct compromises can be made based on any constraints
</details>

### Accessibiliy + Responsive web design

- Increasingly, applications and pages need to be accessible and performant on multiple devices with different capabilities
- Use of media queries allows targeting specific device capabilities
- Not everyone is on a modern phone with a 4G connection
- Web applications need to be accessible for all types of users

<details>
<summary>Notes</summary>

In the past web pages were designed to be used on desktop or laptop computers, typically with a fairly generous screen size and access to a mouse and keyboard. With the explosion of mobile phones, tablets and wearables, websites and web applications need to function for a wide range of types of users. Additionally, there are better tools availble for users with different abilities particularly users with poor eyesight, or those that might struggle with more common input devices.

With this increase in the use of multiple devices, with different screen sizes, browsers orientations and capabilities, it has become ever more challenging to design and develop web applications and pages that are performant, functional and look good across all devices.

Progress has also been made in cross-browser compatability, with a lot of modern web browsers sharing the same rendering engines, while not always the case, for the most part this has made it easier to ensure developers have the confidence their content looks the same (or close enough) for different users.

It's also _safer_ to now assume the presence of javascript, this was not always the case previously and required lots of workarounds to ensure a webpage still functions, while diminshed now, this can still be a major limitation in some industries particuarly government and financial institutions.

</details>

### Application architecture

- Data fetching
- Asynchronous (async) communication / events
- Managing application state

<details>
<summary>Notes</summary>
One key area of concern for frontend engineers building an application of any considerable size, is ensuring a sound and extensible application structure.

The architecture of an application can have drastic effects on how maintainable it is, how easy it is to bring on new team mates into the project to contribute and also how well the application performs.

There are lots of areas related to frontend architecture, but managing application state, fetching data and handling asynchronous effects are all key aspects a frontend engineer at any stage needs to consider when building a web page or application.

There are a myriad of approaches to all of the above, with varying pros and cons, so its good to have a deep understanding of these key concepts.

</details>

#### Data fetching

- AJAX (Asynchronous JavaScript and XML)
- GraphQL

<details>
<summary>Notes</summary>
Fetching data from data sources is a key aspect of frontend engineering. Typically for performance and security, business logic, user data and any sensitive information will be contained in backends with specific APIs to expose the exact data that can be displayed, or to initiate actions on the backend. This can be a mixture of internal or also external 3rd party backends.

AJAX uses a combination of technologies to provide a consistent way to update user interfaces without requiring the full page to be reloaded. Early approaches made use directly of the XMLHttpRequest API which was useful for transferring data between a server without needing a full bwe page refresh, along with the XML format providing a description of any request data and query response, all sequenced by javascript. Modern approaches make use of the Fetch API and the JSON data format to achieve the same goals.

GraphQL is a newer approach to data fetching, while traditional APIs return data in a specific format, often requiring some transformation on the frontend to make it useful, GraphQL use a specific query language allowing clients to query for the exact data they require, in the format they require it provided the backend has a way to _resolve_ where the data should come from.

GraphQL provides a layer of abstraction that provides flexibility and additional control to frontend engineers, and helps to allow for changes to the backend and frontend to be made independently of each other.

</details>

#### Asynchronous (async) events

- User interactions: clicks, mouse over, touch events, scrolling
- Device events: screen orientation change, switching to full screen, network disconnects
- Content related events: all images have loaded, media starts playing, network disconnects

<details>
<summary>Notes</summary>
It's impossible to predict the exact sequence of interactions a user will have with a web applications, therefore its important that web applications can respond to events that could occur at any point in time.

The types of events that can occur depend on the device and the content available on the page, but could be roughly grouped into user interactions and passive events.

</details>

#### Managing application state

<details>
<summary>Notes</summary>
Managing application state for complex frontends has its own set of challenges, typically the state of a frontend refers to the configuration of UI elements currently visible on the screen, any data that has been loaded into memory and as well as actions to support the flow from one state to another.

There are many approaches to managing application state, often new approaches will result in a framework or library providing common patterns, for example the flux pattern as implemented by redux or vuex, which borrows ideas from functional programming, relying on a separations between actions and functions that mutate or change data.

</details>

#### SPAs

- The application loads at once, with dynamic updates made to segments of the page as the user interacts with it
- Provides a more seamless interaction for the users and can appear to be faster than multi page applications
- Common examples: google maps, facebook, trello
- Harder to "deep link" into, or to optimize for SEO

<details>
<summary>Notes</summary>
....

There are a few common approaches to SPAs

- Application root node: rendering a single HTML element that the entire application loads into
- Server side hydration:
- Finally another approach can be to make use of specific target HTML elements where we load smaller applications into, similar to the root node approach but can be useful in situations where a mixture of server and client side rendered content makes sense
</details>

## Key tools and technologies

### HTML + CSS + Javascript

> Image of the triforce with the 3 elements connected

<details>
<summary>Notes</summary>
No matter which specific framework, or tool frontend engineers choose, at the heart of it will be HTML, CSS and javascript.

HTML is the backbone of any webpage, providing a succinct and portable way to describe the structure of a webpage and mark the content for a web browser to display.

CSS provides a powerful way to specifiy how documents are presented, this can include the fonts used, the colors and visual layout of all the elements in the document. It can also be used for more complex presentation logic like animations.

Javascript is the final piece of the puzzle, adding interactivity to web pages, it provides the means to manipulate the HTML document or CSS styling, react to user interactions, initiate actions or requests to fetch additional data.

</details>

### Frameworks and libraries

- Provide a clear and consistent structure to the application
- Help to abstract away some of the common boilerplate for web applications
- Often great for teams and collaboration
- Popular frameworks: React, VueJS and Angular

<details>
<summary>Notes</summary>
There are many approaches to structuring and building frontend websites and applications, which has led to an explosion of frameworks and languages to abstract away some of the boilerplate and give frontend engineers more robust tools to build applications that perform well at scale and are relatively easy to maintain.

At the core, we are still manipulating HTML, CSS and javascript but the approaches and tradeoffs can differ dramatically.

The dominant frameworks at the moment would have to be React, VueJS and Angular. These frameworks have been popularized for building single page applications that perform and scale well. Not long ago jQuery, Backbone, KnockoutJS and Mootools were also popular frameworks, so its not uncommon to come across older products built in these frameworks.

</details>

### Build tools / Bundlers / Task Runners

- Concatentate + minify
- Transpiling + polyfilling
- Linting and static analysis

<details>
<summary>Notes</summary>
Splitting files is great for developers maintaining a project, but leads to multiple requests on the user end, slowing down the time to load a page

### Common challenges

- Performance
- Framework / language churn
- Reliability and safety

## Emerging trends

- PWAs
- JAMStack + SSG
- Compile to JS tools + Webassembly

## Useful resources

### Reading materials

- [A list apart - Responsive web design](https://alistapart.com/article/responsive-web-design/)
- [Mediaqueri.es - Examples of responsive web design](https://mediaqueri.es/)
- [TodoMVC - Todolist implementation in multiple frameworks](https://todomvc.com/)
- [PWAs introduction](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Introduction)
- [SurviveJS - comparison of build tools](https://survivejs.com/webpack/appendices/comparison/)

### Exercise

- Work through this quick list of a11y tips, does the site meet all these requirements?
  - Full checklist available[a11yproject checklist](https://www.a11yproject.com/checklist)
- Pick a website you like, or choose from this list
  - If you have another device available spend some time interacting with the website or application through that (phone, tablet, different computer)
  - For firefox users - use [responsive design mode](https://www.youtube.com/watch?v=qGI27bpCZK4) to test
  - For chrome users - use the [device mode simulator](https://www.youtube.com/watch?v=x8ofsJiELQ0)

### Additional resources

- [MDN](https://developer.mozilla.org/en-US/)
- [Firefox responsive design mode](https://developer.mozilla.org/en-US/docs/Tools/Responsive_Design_Mode)
- [Chrome device simulator](https://developers.google.com/web/tools/chrome-devtools/device-mode)
- [syntax fm](https://syntax.fm/)
- [JS party](https://changelog.com/jsparty)
- https://soundcloud.com/thenewstackmakers/
- [The changelog](https://changelog.com/podcast)
