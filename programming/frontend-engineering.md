# Frontend Engineering

- [Template](https://docs.google.com/presentation/d/124zFVyJXes8XuVViceHw4ZhS6eFCNt1RlBZ3V54viME/edit#slide=id.gb0764ef3d4_0_15)

## Overview

- About me 👋
- What is Frontend Engineering
  - History + Why
  - Understanding users + understanding the business
  - Types of FE?
- Typical role / skills
  - Collaboration + communication (the secret sauce)
  - Application architecture
    - Managing application state
    - Async communication / events
    - Data fetching
  - Responsive web design
- Tools and technologies
  - The triforce: HTML + CSS + JS
  - Languages, frameworks and runtimes
  - Build tools
  - SPAs
    - Application root node
    - Server side hydration
- Challenges
  - Performance
  - Accessibility
    - Framework / language churn
    - Server side rendering
  - Reliability and safety
    - JS time / date / number rounding pain

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
- DX

<details>
<summary>Notes</summary>
In a typically medium to large development team, it is likely there will be frontend engineers that work across various different aspects.

Depending on the company / team size / stage of the product some roles will focus more one area over the others, but generally these are all the types of roles frontend engineers will typically be expected to be able to work across.

Across any of these types of roles, a good understanding HTML, CSS and JS is vital to be able to work effectively.

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

#### DX - Developer experience

> Image of a webpack + eslint + prettier + nodejs

<details>
<summary>Notes</summary>
While not a strictly frontend role, there is often a need in any medium to large team to have frontend engineers working on tooling and infrastructre to help other engineers efficiently and effectively build features or components.

This can often involve a wide range of tasks such as implementing linters to ensure the codebase largely adheres to common standards and automate some of this process, it can also involve building out templates or starters to easily allow new applications to be developed, polyfilling features that might not be supported in all browsers and it can also include configuring build systems to bundle, minify and split all the code to reduce the size of code that is shipped to the user.

While these tasks do not directly impact the user, they can help ensure the development team is able to ship features, consistently and efficiently.

</details>

## Typical role / skills

### Collaboration + communication (the secret sauce)

- Often overlooked as a key skill
- Most Frontend roles will require some collaboration with UX / designers + backend engineers
- The ability to understand requirements and effectifvely articulate constraints will always help avoid misunderstandings

### Application architecture

- Application state
- Data fetching
- Asynchronous (async) communication / events

<details>
<summary>Notes</summary>
One key area of concern for frontend engineers building an application of any considerable size, is ensuring a sound and extensible application structure.

The architecture of an application can have drastic effects on how maintainable it is, how easy it is to bring on new team mates into the project to contribute and also how well the application performs.

There are lots of areas related to frontend architecture, but managing application state, fetching data and handling asynchronous effects are all key aspects a frontend engineer at any stage needs to consider when building a web page or application.

There are a myriad of approaches to all of the above, with varying pros and cons, so its good to have a deep understanding of these key concepts.

</details>

#### Application state

<details>
<summary>Notes</summary>
Managing application state for complex frontends has its own set of challenges, typically the state of a frontend refers to the configuration of UI elements currently visible on the screen, any data that has been loaded into memory and as well as actions to support the flow from one state to another.

There are many approaches to managing application state, often new approaches will result in a framework or library providing common patterns, for example the flux pattern as implemented by redux or vuex, which borrows ideas from functional programming, relying on a separations between actions and functions that mutate or change data.

</details>

#### Data fetching

- AJAX (Asynchronous JavaScript and XML)
- GraphQL

<details>
<summary>Notes</summary>
Fetching data from data sources is a key aspect of frontend engineering. Typically for performance and security, business logic, user data and any sensitive information will be contained in backends with specific APIs to expose the exact data that can be displayed, or to initiate actions on the backend.

AJAX uses a combination of technologies to provide a consistent way to update user interfaces without requiring the full page to be reloaded. Early approaches made use directly of the XMLHttpRequest API with XML providing a description of the query response. Modern approaches make use of the Fetch API and the JSON data format.

GraphQL is a newer approach to data fetching, while traditional APIs return data in a specific format, often requiring some transformation on the frontend to make it useful, GraphQL use a specific query language allowing clients to query for the exact data they require, in the format they require it provided the backend has a way to _resolve_ where the data should come from.

This provides a layer of abstraction that provides flexibility and additional control to frontend engineers, and helps to allow for changes to the backend and frontend to be made independently of each other.

</details>

#### Asynchronous (async) communication / events

- User interaction (clicks, mouse over, touch events, scrolling)
- Passive events (screen orientation change, media start playing, network disconnects)
- Data loading

<details>
<summary>Notes</summary>
</details>

### Accessibiliy + Responsive web design

- Increasingly applications and pages need to be accessible and performant on multiple devices with different capabilities
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

### Collaboration + communication (The secret sauce)

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

#### SPAs

<details>
<summary>Notes</summary>
</details>

## Tools and technologies

### The triforce: HTML + CSS + JS

<details>
<summary>Notes</summary>
At the core of all frontend languages or frameworks is the ability to manipulate, HTML CSS and javascript, these core technologies are how we describe content to a web browser and allow users to accomplish tasks.
</details>

### Languages, frameworks and runtimes

### Build tools

### Monitoring??

### Challenges

- Performance challenges
- Framework / language churn
- Server side rendering
- Reliability and safety

## Emerging trends

- PWAs
- Compile to JS tools
- Functional JS
- Serverless

## Useful resources

- [MDN](https://developer.mozilla.org/en-US/)
- [syntax fm](https://syntax.fm/)
- [JS party](https://changelog.com/jsparty)
- [A list apart - Responsive web design](https://alistapart.com/article/responsive-web-design/)
- [Mediaqueri.es - Examples of responisive web design](https://mediaqueri.es/)
- [a11y - accessibility](https://www.a11yproject.com/)
- https://soundcloud.com/thenewstackmakers/
- https://twitter.com/mouneer/status/1342559926611271681
- [The changelog](https://changelog.com/podcast)
