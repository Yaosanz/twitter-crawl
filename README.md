# Twitter Data Crawling with tweet-harvest

This repository demonstrates how to crawl Twitter data using the `tweet-harvest` package. The instructions below detail the steps required to set up the environment and execute the script to collect tweets.

---

## Prerequisites

Before starting, ensure you have the following:

1. **Python** installed on your system.
2. **Node.js** (v20 or later) for running `tweet-harvest`.
3. A valid **Twitter API Auth Token**.
4. Basic familiarity with terminal/command-line operations.

---

## Steps to Crawl Twitter Data

### 1. Clone This Repository

```bash
git clone https://github.com/your-username/your-repository.git
cd your-repository
```

### 2. Install Required Python Packages

Install the `pandas` library for data manipulation:

```bash
pip install pandas
```

### 3. Install Node.js

Install Node.js as it is required to run `tweet-harvest`:

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=20 && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt-get update
sudo apt-get install nodejs -y
```

### 4. Verify Node.js Installation

Check if Node.js is installed correctly:

```bash
node -v
```

### 5. Configure the Script

Edit the `twitter_auth_token` variable in the script to include your Twitter API Auth Token:

```python
twitter_auth_token = 'your_twitter_auth_token_here'  # Replace with your token
```

Set the search parameters:

- `filename`: The name of the output CSV file.
- `search_keyword`: Your search query (e.g., keyword, date range, language).
- `limit`: The maximum number of tweets to retrieve.

Example:

```python
filename = 'gibran.csv'
search_keyword = 'gibran since:2023-04-01 until:2024-04-01 lang:id'
limit = 100
```

### 6. Run the Script

Execute the script to crawl Twitter data:

```bash
npx -y tweet-harvest@2.6.1 -o "{filename}" -s "{search_keyword}" --tab "LATEST" -l {limit} --token {twitter_auth_token}
```

### 7. Analyze the Data

Load the retrieved data into a Pandas DataFrame for analysis:

```python
import pandas as pd

# Specify the path to your CSV file
file_path = f"tweets-data/{filename}"

# Read the CSV file into a pandas DataFrame
df = pd.read_csv(file_path, delimiter=",")

# Display the DataFrame
display(df)

# Check the number of tweets retrieved
num_tweets = len(df)
print(f"Jumlah tweet dalam dataframe adalah {num_tweets}.")
```

### 8. Output

The script saves the crawled tweets to a CSV file named `gibran.csv` (or the filename you specified). You can find it in the `tweets-data` folder.

---

## Notes

- Ensure your Twitter API Auth Token has the required permissions to retrieve tweets.
- Adjust the `search_keyword` parameter to customize your search query.
- Refer to the [tweet-harvest documentation](https://github.com/grikomsn/tweet-harvest) for more options and usage.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.
