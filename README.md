# Cheap Flight Tracker

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This Python application automates the process of finding cheap flights. It reads your desired destinations and price limits from a Google Sheet, searches for flights using a flight search API (like Kiwi.com), and sends you SMS alerts via Twilio when it finds a flight cheaper than your target price.

## How It Works

1.  **Google Sheet Input:** You maintain a Google Sheet with a list of destinations you want to visit and your maximum acceptable price for flights to those destinations.
2.  **Data Retrieval:** The script fetches this destination data using the Sheety API (or the Google Sheets API).
3.  **Flight Search:** The script queries a flight search API (Kiwi.com) for each destination to find the cheapest flights within the next 6 months.
4.  **Price Comparison:** The script compares the cheapest flight price with your price cutoff from the Google Sheet.
5.  **SMS Alerts:** If a flight is found that's cheaper than your cutoff, the script sends you an SMS notification with the flight details using the Twilio API.

## Prerequisites

* **Python 3.12:** Make sure you have Python 3.6 or a later version installed.
* **Required Python Libraries:** Install the necessary libraries using pip:
    ```bash
    pip install requests twilio google-api-python-client  # You might need other libraries
    ```
* **Google Sheet:**
    * Create a Google Sheet with columns for:
        * `city` (Destination city name)
        * `iataCode` (IATA code for the airport - this can be initially empty and your script will populate it)
        * `lowestPrice` (Your maximum acceptable price for a flight to that city)
* **Sheety API (or Google Sheets API):**
    * If using Sheety, create a project and connect it to your Google Sheet.  Obtain the Sheety API endpoint for your sheet.
    * If using the Google Sheets API directly, you'll need to set up Google Cloud credentials and enable the Google Sheets API.  Follow the Google API documentation for details.
* **Kiwi.com API Account:**
    * Sign up for a developer account at [Kiwi.com](https://developers.kiwi.com/) (or your chosen flight API provider) and obtain your API key.
* **Twilio Account:**
    * Sign up for a Twilio account at [twilio.com](https://www.twilio.com/) and obtain your Account SID and Auth Token.  You'll also need a Twilio phone number.

## Setup

1.  **Clone the Repository (Optional):**
    ```bash
    git clone <https://github.com/Afeez07/Cheap_Flight_Tracker/>
    cd cheap-flight-tracker
    ```
2.  **Install Dependencies:**
    ```bash
    pip install -r 
    ```
3.  **Set Environment Variables:** It's crucial to store your API keys and sensitive information securely.  Use environment variables:
    ```bash
    export SHEETY_PRICES_ENDPOINT="YOUR_SHEETY_API_ENDPOINT"  # Or your Google Sheets API endpoint
    export TEQUILA_API_KEY="YOUR_TEQUILA_API_KEY"
    export TWILIO_ACCOUNT_SID="YOUR_TWILIO_ACCOUNT_SID"
    export TWILIO_AUTH_TOKEN="YOUR_TWILIO_AUTH_TOKEN"
    export TWILIO_PHONE_NUMBER="YOUR_TWILIO_PHONE_NUMBER"  # Your Twilio phone number
    export YOUR_PHONE_NUMBER="YOUR_PERSONAL_PHONE_NUMBER" # The number to send texts to
    ```
    (You might want to set these in your `.bashrc`, `.zshrc`, or use a `.env` file and `python-dotenv`).
4.  **Configure the Google Sheet:** Ensure your Google Sheet is set up correctly with the required columns.
5.  **Implement API Calls:** **Crucially, you MUST implement the actual API calls to Kiwi.com (or your chosen flight API) in `flight_search.py`.** The provided code has a placeholder.  Refer to the API documentation for how to make requests and parse responses.
6.  **Implement Notification Logic:** You **MUST implement the Twilio SMS sending logic in `notification_manager.py`.** Use the Twilio Python library to send formatted flight details.

## Running the Application

1.  Open your terminal.
2.  Navigate to the project directory.
3.  Run the `main.py` script:
    ```bash
    python main.py
    ```
4.  The script will:
    * Fetch data from your Google Sheet.
    * Search for flights.
    * Send you SMS alerts if it finds deals.

## Important Notes

* **API Usage Limits:** Be mindful of the API usage limits of both the flight search API and the Google Sheets API (or Sheety).  Implement delays or error handling to avoid exceeding these limits.
* **Error Handling:** Add robust error handling to make your script more reliable.
* **Date Handling:** Pay close attention to date formatting and calculations when working with the flight search API.
* **Optimization:** For daily execution, optimize your code to run efficiently.  Consider caching data to reduce API calls.
* **Security:** **Never commit your API keys or credentials to your repository** Use environment variables or secure configuration methods.

## Potential Improvements

* **More Flight Details:** Include more flight details in the SMS messages (e.g., departure airport, arrival airport, flight duration).
* **Multiple Alerts:** Allow users to set up alerts for multiple price thresholds or different timeframes.
* **User Interface:** Consider adding a simple command-line interface (CLI) or a web interface to make the application more user-friendly.
* **Email Notifications:** In addition to SMS, support email notifications.
* **Database:** Store flight data in a database for more advanced querying and analysis.
* **Flexible Dates:** Allow users to specify more flexible date ranges for their searches.


## Acknowledgments

* Thanks to [Kiwi.com](https://www.kiwi.com/) (or your chosen flight API provider) for their flight search API.
* Thanks to [Twilio](https://www.twilio.com/) for their SMS messaging API.
* Thanks to Sheety (or Google Sheets API) for providing a way to interact with Google Sheets.
