# CodeSamples-Improving Code Quality

### Introduction
This document outlines the steps I have taken to improve the quality of my code. I have identified several issues with my previous code, including:

1) Unclear logic leading to repeated code
2) Lack of proper component separation
3) No use of TypeScript
4) Overreliance on if-else statements

### Changes Implemented

1) Updating logic to eliminate redundant code and increase code reusability
2) Conducting proper component separation    
3) Utilizing TypeScript
    TypeScript is a statically typed superset of JavaScript that provides features such as type checking, interfaces, classes, and more. The use of TypeScript can improve the development experience in several ways:
    1) Enhanced tooling: TypeScript integrates well with modern development tools, making it easier to write, test, and debug code.
    2) Improved code quality: With TypeScript, you can catch type-related errors at compile-time instead of runtime. This can result in fewer bugs and easier maintenance.
    3) Better scalability: TypeScript allows you to write modular, scalable code with features like interfaces and classes.
    4) Better collaboration: TypeScript's type system provides clear documentation for the code, making it easier for other developers to understand and collaborate on a project.
  
4) Redux Toolkit for State Management
   * I utilize Redux to maintain all the states within a single immutable object, which simplifies state management for the entire application and ensures predictability and scalability.
   * Compared to Redux:
      1) Significantly less boilerplate code is needed
      2) Setting up thunks for async operations is no longer necessary, as createAsyncThunk is included for handling async request cycles.
      3) Plenty of hooks are available, such as useSelector for selecting from the state and useDispatch for dispatching actions.
5) More Unit testing and automation testing
   1) For the end users to have a better quality user experience and ensure the robustness of the application, e2e and unit testing is always good to have. (e.g. Cypress, Selenium)
6) Pre-render
   1) To optimize user experience, several pre-rendering options are available to reduce the time for the First Contentful Paint and First Meaningful Paint.
    ##### Static Site Generator (SSG) vs Server Site Rendering (SSR).
   2) If all users see the same content on the first page, it is better to use SSG instead of SSR as it is more predictable. During the code deployment to production, the production build already has the HTML file rendered for the first page.

### Considerations

While good examples may also have their limitations, I am committed to continuous learning and improvement to enhance the quality of my code.

### Conclusion
This document serves as an overview of the changes I have made to improve the quality of my code. I hope that these changes will result in more readable, maintainable, and extensible code.
