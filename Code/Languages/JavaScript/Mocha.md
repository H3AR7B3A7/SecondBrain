# Mocha
[Official Web Pages](https://mochajs.org/)
Mocha is a feature-rich [[JavaScript]] test framework running on Node.js and in the browser, making asynchronous testing simple and fun. Mocha tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases.

### Create Project
Navigate to the desired directory, and:
>npm init  
>npm install --save-dev mocha chai

Create a 'test' folder and edit *package.json* to use Mocha:

    "scripts": {
        "test": "mocha"
    }

## Running Tests
>mocha test  
>npm test  
>mocha --reporter min  
>mocha --reporter markdown  
>mocha --reporter nyan

Or we can automate running the test on saving the file:
>mocha --watch ./test/ship_test.js ./game_logic/game_methods.js

Or edit *package.json*:

    "scripts": {
        "test": "mocha"
        "test:watch": "mocha --watch ./test ./"
    }

To have Mocha watch all files:
>mocha:watch

To stop Mocha from watching:
>Ctrl + C



---
#JavaScript #Testing