---
layout: post
title: Numbers Generator
categories: [programming]
tags: [ruby, rails, api, ]
shortinfo: |
  Sometimes we need a service that generates all the numbers from 1 to N... So, this web service returns all the numbers from 1 to the user's choice as a JSON array. It also has a client where you test it or use it to generate these numbers.<br><br>
image: /assets/media/numbers.png
---

Sometimes we need a service that generates all the numbers from 1 to N... So, this web service returns all the numbers from 1 to the user's choice as a JSON array. It also has a client where you test it or use it to generate these numbers.

# Server

* Ruby version
  > 2.4.0

* Deployment instructions
  - `bundle install`
  - `bundle exec rails s`
  - Visit `localhost:3000/numbers/[:number]`

* To run the tests, just run
  - `bundle exec rspec`

## Code explanation
### Controller
[`app/controllers/numbers_controller.rb`]

Renders the valid array only if we got a valid response from the method `serial` of `NumberService`, otherwise it renders nothing with status `400`.

### Service
[`app/services/number_service.rb`]

This service has two public methods and one private. The private method `valid_integer` validates if the number that we received is not a string and if it is smaller than the maximum Integer that Ruby can handle.

The public method `serial` is the one that returns the array containing all the numbers from 1 to N. It will return the array only if the number is valid.

The public method `as_json` gives a `Hash` format to the answer.

### Specs
[`spec/controllers/numbers_controller_spec.rb`]
[`spec/services/number_service_spec.rb`]

Using rspec, this project is testing the possible calls to the controller and all the public methods of the service. This is also being tested by TravisCI.

## API Resource
- [GET /numbers/[:number]]

### GET /numbers/[:number]
Example: https://serene-meadow-78539.herokuapp.com/numbers/12

Response body:
```
{
      "numbers": [
          1,
          2,
          3,
          4,
          5,
          6,
          7,
          8,
          9,
          10,
          11,
          12
      ]
  }
  ```

The code is hosted on :octocat: and hosted on heroku. Here is the repository: [https://github.com/isabel22/numbers-server](https://github.com/isabel22/numbers-server).

# Client

This is a simple client to test the service provided before.

## Local test
1. Download the file `index.html`
2. Open the file (you can just double click on it)
3. Enter a number in the field
4. Press the `Submit` button
5. The result will be shown at the bottom

## Online test
1. Visit https://isabel22.github.io/numbers-client/
2. Enter a number in the field
3. Press the `Submit` button
4. The result will be shown at the bottom

The code is hosted on :octocat:. Here is the repository: [https://github.com/isabel22/numbers-client](https://github.com/isabel22/numbers-client).

This client is hosted on [GitHub Pages](https://pages.github.com/): [https://isabel22.github.io/numbers-client/](https://isabel22.github.io/numbers-client/)

![numbers-generator](/assets/media/numbers.png)
