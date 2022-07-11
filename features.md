# Features

Tetikus provides several features that can help you build a more maintainable automated tests codebase.

## Parallel Run
Tetikus runs tests you create in parallel, based on driver configuration that you provide. If you provide driver configuration for mobile and web driver, then Tetikus will run tests for both platform simultaneously.

This feature is currently the default mode for test run and not configurable.

## Unified Element
```java
@BaseURL("https://www.medium.com")
public class WebsitePage extends PageObject {
    @Locator(webXPath = "//a[text()='Sign In']",
            mobileID = "com.medium.reader:id/sign_in_prompt")
    private Element signInButton;

    @Locator(webXPath = "//div[text()='Sign in with Twitter']",
            mobileID = "com.medium.reader:id/sign_in_twitter_button")
    private Element signInWithTwitterButton;

    public void goToTwitterLoginPage() {
        signInButton.waitUntilClickable().click();
        signInWithTwitterButton.waitUntilClickable().click();
    }
}
```
Class example above uses Tetikus' Element class that supports for both platform. For commands that you want to invoke for specific platform, Tetikus provides `MobileElementFunction` and `WebElementFunction`.

## Page Object


## Driver Configuration

