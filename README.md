# Stock-Market-Sentiment-Analysis-Using-LLMs
This project demonstrates stock market sentiment analysis using Python, Google's Gemini LLM, and news headlines scraped from Yahoo Finance. It showcases an end-to-end workflow beginning with environment setup and Gemini API configuration.

Step 1: Install Necessary Libraries

Goal: To get the required Python tools (libraries) for web scraping, handling data, interacting with the Gemini API, and plotting.
Action: We used the pip install command to download and install google-generativeai, pandas, requests, beautifulsoup4, matplotlib, and plotly.
Outcome: All the necessary software tools were added to our Colab environment.

Step 2: Adjust Pandas Version

Goal: To fix a compatibility warning where the newly installed pandas library conflicted slightly with a built-in Colab package.
Action: We used pip install pandas==2.2.2 to force the installation of the specific version Colab preferred.
Outcome: The potential conflict was resolved, ensuring smoother operation within Colab.

Step 3: Configure Gemini API Key

Goal: To securely connect our code to Google's Gemini Large Language Model so we could use it for analysis.
Action: We imported the google.generativeai library, provided your unique API key (replacing the placeholder), and configured the library using genai.configure(). We also selected the specific Gemini model (gemini-1.5-flash) to use.
Outcome: Our code was successfully authenticated and ready to send requests to the Gemini API.

Step 4 (Multiple Versions): Define the Web Scraping Function

Goal: To create a reusable piece of code (a function named Workspace_yahoo_finance_news) that could automatically visit the Yahoo Finance news page and extract relevant news headlines and their web links.
Action: We defined the function using requests (to fetch the webpage) and BeautifulSoup (to parse the HTML). We had to revise this function three times (v1, v2, v3) because the structure of the Yahoo Finance website kept changing, and our initial attempts didn't grab the correct headlines. The final successful version (v3) targeted link (<a>) tags directly and filtered them based on their URL and text content.
Outcome: We had a working function capable of fetching a list of actual news headlines and links from Yahoo Finance.

Step 5 (Multiple Versions): Test the Web Scraping Function

Goal: To actually run the Workspace_yahoo_finance_news function and check if it was successfully retrieving the news data we wanted.
Action: We called the function (news_data = fetch_yahoo_finance_news()) and printed the first few results. We did this after each revision of the function in Step 4.
Outcome: The first two tests showed the scraping wasn't working correctly (getting navigation links or nothing). The test after defining the v3 function successfully returned a list (news_data) containing real headlines and links (we got 11 headlines).

Step 6: Define the Sentiment Analysis Function

Goal: To create a function (analyze_sentiment) that could take a single piece of text (a headline) and ask the configured Gemini model whether the sentiment was Positive, Negative, or Neutral.
Action: We defined the function. Inside it, we created a specific prompt instructing Gemini to classify the sentiment and return only one word. It then used model.generate_content() to send the prompt and headline to the API and processed the response.
Outcome: We had a function ready to analyze the sentiment of any given headline using Gemini.

Step 7: Test the Sentiment Analysis Function

Goal: To make sure the analyze_sentiment function was working correctly and communicating with the Gemini API as expected.
Action: We called the function with a sample positive headline and a sample negative headline and printed the results.
Outcome: The function correctly returned "Positive" for the positive example and "Negative" for the negative example, confirming it worked.

Step 8: Define the News Processing Function

Goal: To create a function (classify_news) that could handle the entire list of news items (news_data) returned by the scraper. It needed to loop through each item, call analyze_sentiment on its headline, and collect all the results.
Action: We defined the function. It took the list of news as input, iterated through it, called analyze_sentiment for each headline, stored the headline, link, and resulting sentiment in a temporary list, and finally converted that list into a Pandas DataFrame (a table structure).
Outcome: We had a function ready to process our list of scraped news and organize the sentiment results into a table.

Step 9: Process Scraped News and Create DataFrame

Goal: To actually use the classify_news function on the real news_data we scraped in Step 5 (v3) and see the final, analyzed results in a table.
Action: We called classify_news(news_data) and stored the resulting DataFrame in the df_news_sentiment variable. We then printed this DataFrame.
Outcome: We obtained a Pandas DataFrame containing the 11 scraped headlines, their links, and the corresponding sentiment (Positive, Negative, or Neutral) assigned by Gemini for each one.

Step 10: Define the Visualization Function

Goal: To create a function (plot_sentiment_distribution) that could take the DataFrame of results and automatically generate a bar chart showing how many headlines fell into each sentiment category.
Action: We defined the function using matplotlib.pyplot. It calculated the counts of each sentiment in the DataFrame's 'Sentiment' column and used .plot(kind='bar') to create the visualization with labels and a title.
Outcome: We had a function ready to create a visual summary of the sentiment results.

Step 11: Visualize the Sentiment Distribution

Goal: To actually generate and display the bar chart summarizing the sentiment analysis results from our DataFrame.
Action: We called the plot_sentiment_distribution(df_news_sentiment) function.
Outcome: A bar chart was displayed, visually showing the distribution (5 Positive, 4 Negative, 2 Neutral) of sentiments for the analyzed headlines.

(Optional) Step 12: Save Results

Goal: To save the DataFrame containing the headlines, links, and sentiments to a file for later use, avoiding the need to re-scrape and re-analyze.
Action: We used the .to_csv() method on our DataFrame (df_news_sentiment.to_csv('yahoo_news_sentiment.csv', index=False)).
Outcome: The analyzed data was saved into a CSV file named yahoo_news_sentiment.csv in the Colab environment.
