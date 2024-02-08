# AmazonTestingVibhavari
 To Create Repository for rt Camp Assignment using Automation and Manual by vibhavari yadav
#Automation Testing Script
#1. Validate Login 2. Should be able toadd product to cart and perform Checkout Action 3. Validate Search Result 4. Validate Product Whishlist Functionality

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.Test;

public class Amazon {
	WebDriver driver;

	@Test
	public void PositiveLogin() throws InterruptedException {
		// Initialize ChromeDriver
		driver = new ChromeDriver();

		// Maximize the browser window
		driver.manage().window().maximize();

		Thread.sleep(2000);
		// Open Amazon website
		driver.get("https://www.amazon.com/");

		// Click on the sign-in link
		driver.findElement(By.id("nav-link-accountList")).click();

		// Enter username and password
		driver.findElement(By.id("ap_email")).sendKeys("your_email@example.com");
		driver.findElement(By.id("continue")).click();
		driver.findElement(By.id("ap_password")).sendKeys("your_password");
		driver.findElement(By.id("signInSubmit")).click();

		// Verify if login is successful
		boolean isLoggedin = driver.findElement(By.id("nav-link-accountList")).isDisplayed();
		Assert.assertTrue(isLoggedin, "Login failed");
		
		// Search for an item
		WebElement searchBox = driver.findElement(By.id("twotabsearchtextbox"));
		searchBox.sendKeys("Lipstick");
		searchBox.submit();

		// Click on the first search result
		WebElement firstSearchResult = driver.findElement(By.xpath("(//span[@class='a-size-medium a-color-base a-text-normal'])[1]"));
		firstSearchResult.click();

		// Add the item to the cart
		WebElement addToCartButton = driver.findElement(By.id("add-to-cart-button"));
		addToCartButton.click();

		// Wait for the cart count to update
		WebDriverWait wait = null;
		wait.until(ExpectedConditions.textToBePresentInElementLocated(By.id("nav-cart-count"), "1"));

		// Navigate to the cart
		WebElement cartIcon = driver.findElement(By.id("nav-cart"));
		cartIcon.click();

		// Proceed to checkout
		WebElement proceedToCheckoutButton = driver.findElement(By.xpath("//input[@value='Proceed to checkout']"));
		proceedToCheckoutButton.click();

    		//Close Browser
      		driver.quit();
	}
}


