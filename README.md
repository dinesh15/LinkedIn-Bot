# Also, how I run the program is different. 

This project is a Python script that automates sending connection requests on LinkedIn using Selenium and Firefox. The script aims to help you connect with professionals on LinkedIn by automatically searching for people, navigating their profiles, and sending connection requests with a custom message.

## Features

- Search for people on LinkedIn based on keywords.
- Navigate through multiple search result pages to collect profiles.
- Automatically send connection requests with personalized messages.
- Use headless browsing mode to run the bot in the background.
- Load saved profiles from a file to send connection requests later.

## Getting Started

### Prerequisites

- Python 3.x
- Selenium
- Firefox browser
- Firefox GeckoDriver (Automatically managed by `webdriver_manager`)
- `webdriver_manager` library
- Utilities from `utilities.py` and `selenium_firefox.py` modules

### Installation

1. Clone the repository to your local machine.

   ```bash
   git clone https://github.com/your-repository/linkedin-connector-bot.git
   cd linkedin-connector-bot
   ```

2. Install the necessary Python packages.

   ```bash
   pip install -r requirements.txt
   ```

3. Install Firefox browser if not already installed.

4. Run the script using:

   ```bash
   python linkedin_connector.py
   ```

### Usage

- **Search Query**: Modify the `SEARCH_QUERY` variable in the script to specify the target keyword for your LinkedIn search (e.g., "Restaurant owner").
- **Location**: Set the `GEO_URN` value to filter results by geographic location. You can find the GEO\_URN value by searching your location on LinkedIn.
- **Connection Message**: You can customize the message to be sent with each connection request using `MESSAGE_WITH_NAME` or `MESSAGE_WITHOUT_NAME`. The placeholder `{{name}}` is dynamically replaced by the recipient's name.
- **Number of Connections**: Set `N_SEARCH_RESULTS` to determine how many connection requests the bot should send.
- **Headless Mode**: Use the `--headless` flag to run the browser in headless mode.
- **Prompt for Action**: Set `ASK_BEFORE_SENDING` to `True` if you want the bot to ask for your confirmation before sending each connection request.

### Running the Bot
Run the script using:

```bash
python linkedin_connector.py
```

The script will prompt you to enter the LinkedIn URL you want to scrape. You can input any valid LinkedIn search URL or profile URL to begin the scraping process. For example:

```bash
Please enter the LinkedIn URL you want to scrape: https://www.linkedin.com/search/results/people/?keywords=Restaurant%20Owner&geoUrn=103644278
```

The bot will then navigate through the pages, collect profiles, and begin sending connection requests.

For more information about available options, use the `--help` flag:

```bash
python linkedin_connector.py --help
```

## Approach Explanation

This bot interacts with LinkedIn by using the Firefox browser automated with Selenium. Below is an overview of the key components of the approach used in this implementation:

1. **Initialization**:

   - The script initializes the Firefox WebDriver using the GeckoDriver and prepares a customized Firefox profile for LinkedIn login and browsing. It uses the `webdriver_manager` package to ensure the GeckoDriver is managed automatically.

2. **Loading People**:

   - The bot either loads profiles from a saved file or searches LinkedIn using the specified search query and location.
   - The search results are paginated, and the bot navigates through pages to collect profile information.

3. **Sending Connection Requests**:

   - For each collected profile, the bot navigates to the user's LinkedIn profile page.
   - Instead of relying on specific class names for the action container, the bot collects all buttons on the page and checks their accessibility text to determine if they are "Connect", "More", or "Pending" buttons.
   - The bot identifies the appropriate buttons and sends a connection request if it finds the "Connect" button.
   - If the "Connect" button is inside a dropdown menu, the bot clicks the "More" button first to access it.
   - The bot uses JavaScript to click elements when standard Selenium interactions are not sufficient due to overlays or dynamic content.

4. **Adding a Custom Note**:

   - When sending a connection request, the bot can also add a custom message. If the person's company information is available, it is included in the message.

5. **Handling LinkedIn Specifics**:

   - This script includes several features to handle LinkedIn's dynamic nature, such as waiting for elements, adding random sleep times, and retrying if elements are not found initially.

### Differences from Original Code by FujiwaraChoki

The original approach by FujiwaraChoki served as the template and inspiration for this project. The key differences in my approach are:

- **Enhanced Customization**: The script has been updated to include dynamic and personalized messages for each connection, using placeholders like `{{name}}` and `{{company_name}}`.
- **Button Identification**: Instead of relying on specific class names for the action container, my approach iterates over all buttons on the page and identifies them based on their accessibility text, such as "Connect", "More", or "Pending".
- **Dropdown Interaction**: The way the bot handles dropdown interactions has been refined, including JavaScript-based interactions for elements that are blocked by overlays.
- **Robustness**: More conditions and fallback mechanisms have been added to handle potential errors or missing elements when navigating the LinkedIn UI.
- **Command-Line Arguments**: Improved command-line arguments handling for more user-friendly usage and flexibility.

### Credits

The original template for this code was inspired by FujiwaraChoki. The approach, however, has been significantly customized and modified to enhance reliability, add additional features, and improve overall interaction with LinkedIn's evolving user interface.

## Disclaimer

Using automation tools on LinkedIn can violate LinkedIn's terms of service. Use this bot responsibly, and understand the risks, including the possibility of your account being restricted or banned. This project is intended for educational purposes only.

## Author

Pampati Dinesh Raj
