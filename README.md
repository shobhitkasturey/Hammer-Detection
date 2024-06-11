Certainly! Here is a README for your project.

---

# Hammer Candlestick Pattern Detector

This project is designed to identify hammer candlestick patterns in a given dataset of candlestick data. The hammer pattern is typically a bullish reversal pattern that indicates a potential bottom in the market.

## Project Overview

The script processes a CSV file containing candlestick data and adds a column indicating whether each candlestick is a hammer. It then filters out the rows where the hammer pattern is detected and saves them to a new CSV file.

## Prerequisites

- Python 3.x
- pandas

## Installation

1. Clone the repository or download the script files.
2. Ensure you have Python 3.x installed on your machine.
3. Install the required Python packages using pip:
    ```sh
    pip install pandas
    ```

## Usage

1. Place your input CSV file (`candlesticks.csv`) in the same directory as the script. The CSV file should have the following columns: `Open`, `High`, `Low`, `Close`.
2. Run the script. This can be done via command line:
    ```sh
    python detect_hammer.py
    ```
3. The script will process the data and generate a new CSV file (`hammers.csv`) containing only the rows where a hammer candlestick pattern is detected.

## Script Explanation

The script performs the following steps:

1. **Load Data**: Reads the input CSV file into a pandas DataFrame.
    ```python
    import pandas as pd

    csv_file = 'candlesticks.csv'
    df = pd.read_csv(csv_file)
    ```

2. **Define Hammer Detection Function**: Checks each row to see if it meets the criteria for a hammer pattern.
    ```python
    def is_hammer(row):
        body = abs(row['Close'] - row['Open'])
        lower_shadow = abs(min(row['Open'], row['Close']) - row['Low'])
        upper_shadow = abs(max(row['Open'], row['Close']) - row['High'])
        
        is_hammer = lower_shadow >= 2 * body and upper_shadow <= body
        return is_hammer
    ```

3. **Apply the Detection Function**: Applies the function to each row in the DataFrame to create a new column `Hammer`.
    ```python
    df['Hammer'] = df.apply(is_hammer, axis=1)
    ```

4. **Filter Hammer Patterns**: Filters out rows where the hammer pattern is detected.
    ```python
    hammers = df[df['Hammer']]
    ```

5. **Save the Results**: Saves the filtered DataFrame to a new CSV file.
    ```python
    hammers.to_csv('hammers.csv', index=False)
    ```

6. **Print the Results**: Prints the first few rows of the detected hammer patterns.
    ```python
    print(hammers.head())
    ```

## Example

Assuming your `candlesticks.csv` looks like this:
```
Open,High,Low,Close
100,110,90,105
105,115,95,110
110,120,105,115
115,125,105,120
...
```

After running the script, `hammers.csv` will contain only those rows that match the hammer pattern criteria.

## Notes

- Ensure the input CSV file is correctly formatted with the required columns.
- Modify the script if your CSV file has different column names or additional columns.

---

