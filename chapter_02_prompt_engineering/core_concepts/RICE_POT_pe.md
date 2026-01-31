Role :   you are a QA automation tester with 15 years of experience. You have a very good understanding of IT, CRM projects like salesforce.com. You need to create a framework with Selenium, Java, Maven, TestNG, and it should be enterprise-level framework that we need to create.



I  - Instructions

- Generate a Complete Selenium with Java automation script following the standard of enterprise level standards.
- Automate and verify the results of the login page [﻿login.salesforce.com/?locale=in](https://login.salesforce.com/?locale=in), ensure that UI is thoroughly tested with valid and invalid testcases.
- [Critical] - Apply the TestNG annotations, @Test, @BeforeTest and others and and necessary setup/teardown logic.
- [Critical] Implement robust exception handling within both Page Object model and test scripts using structured try–catch blocks or explicit exception signatures. 
- [Mandatory] Use Page Object Model with PageFactory, including @FindBy, constructor initialization, and reusable action methods. 
- [Mandatory] - It is important that you use only the xpath not the css selectors. 
- [Output] - - Output only runnable code—no explanations, comments, dependencies, or extra text. 
- [Don't] - Don't use the css selectors, ID, name and others things.
- [Don't] - Don't add comments, Thread.sleep and other bad coding practice.
- [Generate] - Generate the 2 scritps only with the valid and invalid testcases of the login page.
- [DoNOTuse] Thread.sleep() anywhere; rely on WebDriverWait or implicit waits. 
- Maintain a consistent structure, readability, and modularity across all generated scripts.


C — Context
You are creating a login page scripts with proper framework for the sales force login, which is a AB Testing website with valid and invalid login page
where in the login page you have the email, password and submit buttin with remember me fucntionality. 



E — Example
Example structure for PageFactory:

public class LoginPage {
 @FindBy(xpath = "//input[@id='username']")
 WebElement username;



@FindBy(xpath = "//input[@id='password']")
WebElement password;

@FindBy(xpath = "//input[@id='Login']")
WebElement loginButton;

public LoginPage(WebDriver driver) {
    PageFactory.initElements(driver, this);
}

public void doLogin(String user, String pass) {
    username.sendKeys(user);
    password.sendKeys(pass);
    loginButton.click();
}



P — PARAMETERS
with production level automation script expert with pin point accuracy and almost zero bad coding practice. 

O — Output
Provide only: 

- 1 Page Object file 
- 2 TestNG test scripts
1. Maven project
No explanations or additional content.
T — Tone
Technical, precisly, enterprise-grade, code-one.



