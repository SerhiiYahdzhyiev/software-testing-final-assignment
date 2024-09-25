# Test Plan for SY Commerce Application

Table Of Contents:

1. [Introduction](#introduction)
    - [Objective](#objective)
    - [Scope](#scope)
    - [Out Of Scope](#out-of-scope)
2. [Items](#items)
    - [Frontend](#frontend)
    - [Backend](#backend)
3. [Strategy](#strategy)
    - [Levels](#levels)
    - [Manual Testing](#manual-testing)
    - [Security Testing](#security-testing)
    - [Static Testing](#static-testing)
    - [Coverage Focus](#coverage-focus)
4. [Test Cases](#test-cases)
    - [Overview](#overview)
    - [Techniques](#techniques)
5. [Test Execution](#test-execution)
    - [Environment](#environment)
    - [Exectuions](#execution)
    - [Documenting](#documenting)

## Introduction

### Ojbective

The objective of this plan is to ensure that target application meets original
requirements from Assessment Brief by detecting any defects and ensuring that
it performs as expected across key required functionalities. The focus will be
on verifying the core areas of user- and product- management, shopping cart,
orders and checkout.

### Scope

Testing will cover the primary user actions, including browsing products,
adding them to shopping cart, creating order, viewing orders history.
Both frontend and backend components will be tested, however the focus will be
shifted a bit towards backend. The key will areas include:

    - User management (registration, login).
    - Product search and details view.
    - Shopping cart management.
    - Orders creation.
    - Orders history view.
    - Admin functionalities related to products management (mostly creation of
      new product items)

These areas are based on the original assessment brief that defined minimal
requirements for the target application functionalities and features.

Shopping cart functionality was an extra feature, and was not mentioned in the
original requirements, however it is implemented and it is one of the key
components of the functioning application.

### Out of Scope

Certain third-party integrations, such as PayPal payments and other extra
functionalities, will only be tested at a basic level or not tested at all.
This test plan focuses on the minimal requirements thus will not include:

    - Admin functionalities related to users management.
    - Admin functionalities related to orders management.
    - Some extra admin functionalities related to products management aside creation.

## Items

Folllowing key functionalities will be tested:

### Frontend

    - User Management
        - Login/Logout
        - Registration
    - Products
        - Search by title
        - View details
    - Shopping Cart
        - Add/remove products
        - Update Quantities
        - Correct Total Price Calculation
    - Orders
        - Creation
        - History View

### Backend

    - User Management
        - Login/Logout
        - Registration
        - Authentication
        - Token
        - Secure credentials storing
    - Product Management
        - Creation
        - Updating
    - Orders Management
        - Creation
        - Updating
        - History Aggregation

## Strategy

The test strategy will focus primarily on ensuring the backend of the target
application is rigorously tested through automated (unit and integration)
testing, with minimal use of manual testing techniques.

The frontend will be tested using manual techniques, focusing on static testing
and simple functional tests.

### Levels

Unit Testing

    - Objective: Validate that individual functions, methods, and services in
      the backend perform as expected. Targets:
        - User management (registration, login, authentication).
        - Product management (creation, updates).
        - Order management (creation, updating, and history retrieval).

    - Approach: Automated unit tests will be written with
      [vitest](https://vitest.dev/) to cover key business logic.
      Targets:
        - Correct responses from service methods.
        - Handling of edge cases and invalid inputs.
        - Token generation and authentication mechanisms. 

Integration Testing (Backend)

    - Objective: Verify that various backend parts interact correctly together.
      Will focus on:
        - Interactions between services, such as order creation updating user
          order history.
        - End-to-end tests between the API and the database.
        - Icoming data validation (addresses security).

    - Approach: Automated integration tests will be written using vitest or
      another compatible tool. Will focus on:
        - Endpoints for user management, product management, and order
          processing.
        - Validation of data flow between the API and the database.
        - Ensuring proper handling of API requests and responses.

### Manual Testing

Objective: Ensure that the frontend core components work as expected through basic manual
functional testing and static code reviews.

Approach:
    - Functional Testing: Manually test core frontend features, including:
      - user registration,
      - login,
      - product search,
      - shopping cart management,
      - order placement.

    - Static Testing: Review the code for the following:
        - Ensure proper component structure and separation of concerns.
        - Code quality checks (e.g., linting, formatting).

    - Visual Inspection: Validate the UI/UX manually by reviewing the site
      for any:
          - layout issues,
          - incorrect data display,
          - typos,
          - responsiveness across different devices.

### Security Testing

Objective: Ensure that the backend handles sensitive information securely,
using static analysis (code review).

Approach:
    - Source Code Review: Verify that secure coding practices are followed,
      including:
        - Correct salting, hashing, and peppering of passwords using proper
          tooling.
        - Proper management of JWT tokens and session data.
        - Secure handling of user input to avoid injection attacks (e.g.,
          SQL/NoSQL injection).

    - Manual Inspection: Check the application for potential security
      vulnerabilities, such as:
        - Lack of HTTPS/SSL or improperly configured CORS policies.
        - Insecure storage of sensitive data (f.e. hardcoded tokens or
          credentials).

### Static Testing

Objective: Evaluate the ease of use and UI/UX quality through static and
visual review methods.

Approach:
    - Code Reviews: Manually inspect codebases for maintainability, structure,
      and best practives.
    - UI Review: Test the application’s responsiveness, layout, and
      accessibility across different devices and browsers.

### Coverage Focus

Priority will be given to automated tests, covering key
business logic and API interactions.

Static code reviews and manual testing will be performed to ensure
essential functionality and visual aspects working correctly.

Emphasis on static techniques for security assessments, focusing on reviewing
sensitive data handling and secure coding practices.

## Test Cases

### Overview

The test cases are designed to ensure that the minimal required
functionalities of the target application work as expected.
Automated tests will focus on the application server logic and API
interactions, while manual tests will cover critical interface scenarios,
primarily around price calculations during order creation and in the
shopping cart.

*NOTE: User management functionalities should also be covered by the test cases
for both parts of the application, despite the fact that they where not
mentioned in the initial requirements, but where realized thous becomming one
of the critical/vulnerable points.

### Techniques

- `Black-box Testing` such as: 
    - *Equivalence Partitioning*
    - *Boundary Value Analysis*

- `Static Testing` such as:
    - *code reviews*
    - *UI inspection*

Thanks for the detailed input! Based on your responses, here’s the draft for the **Test Execution** section, structured as per your requirements.

## Test Execution

### Environment

The testing environment will consist of tools and configurations necessary for
both *automated* backend testing and *manual* frontend testing.

#### Backend Testing

- *Vitest*:

  Automated unit and integration tests will be executed using *Vitest*, a
  testing framework compatible with *TypeScript*. Vitest will handle all
  backend service, API, and logic tests.

- *In-memory MongoDB Mock*:

  For simulating the database during tests, *Mongo Memory Server* will be
  used to mock the MongoDB instance, enabling fast and isolated testing without
  interacting with the live database.
  The project source repository also already holds some initial data to populate
  the DB on first launch, they will be reused for setting up the testing
  evironment.

- *Node.js*:

  The backend is written in *Node.js* with Express.js, and tests will be
  executed in the local development environment.

  Proper env will be configured by corresponding environment variable.

#### Frontend Testing

- **Manual Testing Tools**:

  - The *Angular CLI* provides testing tools for component-level tests,
    though (but be omitted during this plan execution)..

  - Manual tests will be executed using a *Chromium-based browser*, with no
    cross-browser testing as it was not part of the original requirements,
    which was used as *Test Basis* for this plan.

### Execution

The testing process will be split into two main parts: 
- automated tests for the backend
- manual tests for the frontend.

#### Backend Testing (Automated)

- *Automated Unit and Integration Tests*:

  Unit and integration tests for the backend will be executed manually via the
  **Vitest** command-line interface. These tests will cover key backend
  functionalities such as user registration, login, product management, and
  order processing.

  Each test run will generate detailed test logs, which will be saved in plain
  text format and stored in the designated repository.

#### Frontend Testing (Manual)

- *Functional Tests*:

  Core functionalities such as product search, cart management, and order
  placement will be tested manually by interacting with the website in the
  browser (Chrome or Firefox). These tests will focus on user actions and price
  calculations in the shopping cart and during checkout.

- *Static Testing*:

  A static code review of the frontend will be conducted to ensure that best
  practices are followed for component structure, styling, and security (e.g.,
  secure handling of sensitive data).

Both *automated* and *manual* tests will be executed manually as needed,
with no automation for test execution scheduling. However, later in the project
lifecycle it will be planned to provide dedicated CI/CD pipelines for
regression testing before deployment stage.

### Documenting

All test outputs will be documented and organized within the repository.
Documentation will include both *automated test logs* 
and *manual test outputs*.

#### Automated Test Logs

- *Backend Test Logs*:

  Output from *Vitest* runs will be stored as plain text log files. Each log
  file will match the corresponding test case and will be named accordingly
  (e.g., `user-registration-test.log`), allowing for easy reference during
  evaluation.

  These logs will be stored in a dedicated repository's corresponding
  directories.

#### Manual Test Documentation

- *Screenshots*:

  For manual tests, screenshots will be captured at critical points during the
  test execution (e.g., after cart updates or order completion). Each
  screenshot will be labeled based on the test case it corresponds to and
  stored in a structured collection within dedicated repository.

  Example naming: `order-total-checkout.png` or `cart-price-update.png`.

- *Structure*:

  Both the automated logs and manual screenshots will be organized by test case
  name to facilitate easy navigation and review by the evaluator(s).
