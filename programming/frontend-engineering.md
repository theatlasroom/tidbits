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
  - APIs (data sources)
  - Languages, frameworks and runtimes
  - Build tools
  - SPAs
    - hybrid (loading an applcation on a specific DOM node)
    - server rendered
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
<summary>Notes</summary
Some frontend engineer role are more focused on the user side, this might require tasks such as development of reuseable components like buttons, form fields and layouts that adhere to the branding and style guidelines for the company.

Often in these kind of scenarios, the engieenrs will work closely with UX researchers and designers to develop components. These components provide an important framework for other engineers to quickly prototype and build new interfaces, without having to worry if the interfaces they are building are consistent with other parts of the website or application.

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

This can often involve a wide range of tasks such as implementing linters to ensure the codebase largely adheres to common standards and automate some of this process, it can also involve building out templates or starters to easily allow new applications to be developed and it can also include configuring build systems to bundle, minify and split all the code to reduce the size of code that is shipped to the user.

While these tasks do not directly impact the user, they can help ensure the development team is able to ship features, consistently and efficiently.

</details>

## Typical role / skills

### Collaboration + communication (the secret sauce)

- Often overlooked as a key skill
- Most Frontend roles will require some collaboration with UX / designers + backend engineers
- The ability to understand requirements and effectifvely articulate constraints will always help avoid misunderstandings

### Application architecture

- SPAs
- Application state
- Asynchronous (async) communication / events

<details>
<summary>Notes</summary>
One key area of concern for frontend engineers building an application of any considerable size, is ensuring a sound and 
</details>

#### Application state

<details>
<summary>Notes</summary>
Managing application state for complex frontends has its own set of challenges, typically the state of a frontend refers to the configuration of UI elements currently visible on the screen, any data that has been loaded into memory and as well as actions to support the flow from one state to another.

There are many approaches to managing application state, often new approaches will result in a framework or library providing common patterns, for example the flux pattern as implemented by redux or vuex, which borrows ideas from functional programming, relying on a separations between actions and functions that mutate or change data.

</details>

#### Data fetching

<details>
<summary>Notes</summary>
</details>

#### Asynchronous (async) communication / events

<details>
<summary>Notes</summary>
</details>

### Responsive web design

- Increasingly applications / websites need to be accessible and performant on multiple devices
- Directly impacts the functionality available and how the designs are implemented
- This also starts to crossover with more performance related issues like bundle size
- While not always the case, we are in a situation where it is _safer_ to assume the presence of JS and a more modern browser, but this can still be a major limitation in some industries

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
- https://soundcloud.com/thenewstackmakers/
- https://twitter.com/mouneer/status/1342559926611271681
- [The changelog](https://changelog.com/podcast)
