# Features

Tetikus provides several features that can help you build a more maintainable automated tests codebase.

## Parallel Run
Tetikus runs tests you create in parallel, based on driver configuration that you provide. If you provide driver configuration for mobile and web driver, then Tetikus will run tests for both platform simultaneously.

This feature is currently the default mode for test run and not configurable.

## Unified Element
```java
    @Locator(webXPath = "//div[text()='Sign in with Twitter']",
            mobileID = "com.medium.reader:id/sign_in_twitter_button")
    private Element signInWithTwitterButton;
```
Example above uses Tetikus' Element class that supports for both platform. For commands that you want to invoke for specific platform, Tetikus provides `MobileElementFunction` and `WebElementFunction` classes.

## Page Object
```java
@BaseURL("https://www.medium.com")
public class WebsitePage extends PageObject {
}
```
PageObject class can be used to apply Page Object design pattern in your codebase. Driver instance would be automatically provided when extending PageObject by using `getWebDriver()` or `getMobileDriver()` methods. 

URL can also be provided as annotation so that you can use `openPage()` method inside the class to open the webpage. This annotation would only run for Web platform.

## Driver Configuration
```json
[
  {
    "platform": "MOBILE",
    "url": "http://127.0.0.1:4723/wd/hub",
    "desiredCapabilities": {
      "automationName": "UiAutomator2",
      "platformName": "Android",
      "udid": "emulator-5554",
      "appPackage": "com.medium.reader",
      "appActivity": "com.medium.android.donkey.start.SplashActivity"
    }
  },
  {
    "platform": "WEB",
    "location": "LOCAL",
    "browser": "CHROME"
  }
]
```

Driver configuration is where you put information regarding location of browsers or mobile that you want to test.

For Web platform, using `"location": "LOCAL"` would trigger WebDriver to instantiate the webdriver on local machine. If you want to test with browsers on remote machine, then you can use `"location": "REMOTE"` and fill the URL and DesiredCapabilities information with the same structure as Mobile configuration example.

