# d2k_newyork_taxi_data_processing
Importing necessary libraries

The code starts by importing three libraries:

requests: This library is used to send HTTP requests to the URL where the data is hosted. It's used to download the CSV files.
os: This library is used to interact with the operating system, specifically to create a directory to store the downloaded files.
datetime and timedelta: These libraries are used to work with dates and times, but they're not actually used in this code snippet. They're likely leftovers from a previous version of the code.
Defining constants and variables

The code defines several constants and variables:

base_url: This is the base URL where the data is hosted. In this case, it's https://s3.amazonaws.com/nyc-tlc/trip+data/.
year: This is the year for which we want to download the data. In this case, it's 2019.
months: This is a range of months from 1 to 12, which will be used to construct the URLs for each month's data.
data_dir: This is the directory where the downloaded files will be saved. In this case, it's a directory named "data" in the current working directory.
Creating the data directory

The code checks if the data_dir directory exists, and if not, it creates it using the os.makedirs() function. This ensures that the directory is present before we start downloading files.

Defining the download function

The code defines a function called download_file() that takes two arguments:

url: The URL of the file to be downloaded.
filename: The local filename where the downloaded file will be saved.
The function does the following:

It sets a retries variable to 3, which will be used to retry the download if it fails.
It enters a loop that will run up to 3 times.
Inside the loop, it sends a GET request to the specified url using the requests.get() function.
If the request is successful, it opens a file with the specified filename in binary write mode ("wb").
It writes the contents of the response to the file in chunks of 1024 bytes using the response.iter_content() method.
If the download is successful, it prints a success message to the console.
If the download fails, it catches the exception, prints an error message to the console, and decrements the retries variable.
If the retries variable reaches 0, it prints a failure message to the console and exits the function.
Downloading the files

The code then loops through the months range and constructs the URL for each month's data using the base_url and the current month. It also constructs the local filename using the data_dir and the current month.

For each month, it calls the download_file() function with the constructed URL and filename.

How the code works

Here's an example of how the code works:

The code sets year to 2019 and months to a range of 1 to 12.
It creates a directory named "data" in the current working directory.
It loops through the months range and constructs the URL for each month's data, such as https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2019-01.csv.
It constructs the local filename, such as data/yellow_tripdata_2019-01.csv.
It calls the download_file() function with the URL and filename.
The download_file() function sends a GET request to the URL, writes the response to the file, and retries up to 3 times if the download fails.
The code repeats steps 3-6 for each month, downloading the data for each month of 2019.

#### Summary

The code processes a collection of CSV files in a specified directory, reads them into DataFrames, and performs various data manipulation and analysis tasks. It starts by defining the column names and setting up the data directory. Then, it iterates through the CSV files, reads them into DataFrames, and processes each file by handling missing values, converting datetime columns, and deriving new columns for trip duration and average speed. The processed DataFrames are then concatenated into a single DataFrame. Finally, the code aggregates the data to calculate total trips and average fare per day, and prints the resulting data.



