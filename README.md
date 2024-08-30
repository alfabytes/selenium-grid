# Selenium Grid with Docker Compose

This project sets up a Selenium Grid using Docker Compose with multiple Chrome nodes. The Selenium Hub manages the grid, and the nodes run Chrome instances that can be accessed remotely for test automation.

## Prerequisites

- Docker: [Install Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/alfabytes/selenium-grid.git
cd selenium-grid
```

### 2. Run the Selenium Grid

Start the Selenium Grid by running:

```bash
docker-compose up -d
```

This command will start the Selenium Hub and 10 Chrome nodes. The grid will be accessible on port 4444 of your Docker host.

### 3. Access the Selenium Grid Console

You can access the Selenium Grid console to monitor the nodes and sessions:

Open your browser and go to: `http://localhost:4444/ui`

### 4. Connect to the Remote WebDriver

To connect to the Selenium Grid using Remote WebDriver in your tests, configure your WebDriver as follows:

```bash
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.RemoteWebDriver;

import java.net.URL;

public class RemoteWebDriverTest {
    public static void main(String[] args) {
        try {
            ChromeOptions options = new ChromeOptions();
            WebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444/wd/hub"), options);
            driver.get("https://www.example.com");
            System.out.println(driver.getTitle());
            driver.quit();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Additional Information

Selenium Hub Ports:

- 4442: Event Bus Publish Port
- 4443: Event Bus Subscribe Port
- 4444: Web Interface and Grid Hub Port Shared Memory Size: The Chrome nodes are configured with 2GB of shared memory (shm_size: 2gb) to avoid browser crashes due to insufficient memory.
