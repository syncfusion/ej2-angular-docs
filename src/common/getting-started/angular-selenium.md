# Getting Started for Selenium E2E Testing using Protractor

This documents helps us to write `Selenium E2E Testing` using `Protractor`.

## Selenium

Selenium is the most preferred framework for End-to-End (E2E) testing of the web applications. But you cannot use Selenium directly for the dynamic web applications such as Angular.  

Usually, you locate HTML elements using following CSS selectors ID, cClass, attributes, and value in Selenium. But while using with Angular applications, due to synchronization issue, you cannot recognize the ng-model, ng-class, ng-bind, ng-options Angular specific attribute directories using the ordinary CSS selectors.

[`Protractor`](https://www.protractortest.org/#/) is specifically developed to overcome the above problem in Selenium E2E testing for Angular web applications. 

## Protractor

Protractor is a wrapper around the WebDriverJS that is the JavaScript binding for WebDriver API. Protractor is an End-to-End (E2E) testing framework specifically developed to automate Angular web applications with new locator strategies. 

You can find the complete list of Protractor API form this [documentation](https://www.protractortest.org/#/api).

## E2E Test for Angular

Using Protractor, you can test the web application either using `in-build ChromeDriver` of Chrome browser or `Selenium Standalone server`.

### Protractor with ChromeDriver

To setup the Protractor with ChromeDriver, set the `directConnect` property to true in configuration as in the following code block. 

```js
exports.config = {
  allScriptsTimeout: 11000,
  specs: [
    './src/**/*.e2e-spec.ts'
  ],
  capabilities: {
    'browserName': 'chrome'
  },
  directConnect: true,
  baseUrl: 'http://localhost:4200/',
  framework: 'jasmine',
  jasmineNodeOpts: {
    showColors: true,
    defaultTimeoutInterval: 30000,
    print: function() {}
  },
  onPrepare() {
    require('ts-node').register({
      project: require('path').join(__dirname, './tsconfig.json')
    });
    jasmine.getEnv().addReporter(new SpecReporter({ spec: { displayStacktrace: true } }));
  }
};
```
The Angular web application created using Angular CLI will automatically includes the configuration and setup for in-build ChromeDriver Protractor E2E testing with sample test case in it.

Running `npm run e2e` or `ng e2e` will run the test cases. 

### Protractor with standalone Selenium server

To setup the Protractor with Selenium Standalone server:-

1.	Set the `directConnect` to false
2.	Set the `seleniumAddress` to `http://localhost:4444/wd/hub`
3.	Ensure that Selenium server is up before running the test cases. 

The Protractor configuration for Selenium standalone should be as in the following code block. 

```js
exports.config = {
  allScriptsTimeout: 11000,
  specs: [
    './src/**/*.e2e-spec.ts'
  ],
  capabilities: {
    'browserName': 'chrome'
  },
  directConnect: false,
  baseUrl: 'http://localhost:4200/',
  seleniumAddress: 'http://localhost:4444/wd/hub',
  framework: 'jasmine',
  jasmineNodeOpts: {
    showColors: true,
    defaultTimeoutInterval: 30000,
    print: function() {}
  },
  onPrepare() {
    require('ts-node').register({
      project: require('path').join(__dirname, './tsconfig.json')
    });
    jasmine.getEnv().addReporter(new SpecReporter({ spec: { displayStacktrace: true } }));
  }
};
```

To install/update and start the Selenium server, run the following command before running the testcases and maintain the server in active state until the testing is finished. 

```cmd
webdriver-manager update
 
webdriver-manager start
```

### Using EJ2 in Protractor 

The Syncfusion Angular EJ2 Components are accessed using the Protractor locators such as ID, css, name and so on. The following code samples explains how the EJ2 button component is used in Protractor testing.
 
## EJ2 Angular Button in `./src/app/app.component.html`

```html
<button id="my_button" ejs-button>Button</button>
```

### Getting EJ2 Element using Protractor Locator `./e2e/src/app.po.ts`

```js
element(by.id('my_button')).getText()
```

### Checking the Actual and Expected Value `./e2e/src/app.e2e-spec.ts`

```js
import { AppPage } from './app.po';

 it('should display welcome message', () => {
    page.navigateTo();
    // console.log(page.getTitleText());
    expect(page.getTitleText()).toEqual('BUTTON');
  });
```