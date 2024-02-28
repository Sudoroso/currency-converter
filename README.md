# API Currency-converter
#### Video Demo:  <https://youtu.be/yu4vLtpxYCQ>
#### Description:

An API that provides real-time currency data from Open Exchange Rates.
It offers information on exchange rates, historical data, and lists of
currency symbols, including insights into alternative digital currencies.
Check it out for quick and easy currency details!

After running the program, you will be prompted to select from one of
the four available functions. The prompt will continue until you decide
to close the program using Ctrl + D.

\### 1. Latest Function The \'latest\' function enables you to retrieve
the most recent exchange rates from the Open Exchange Rates API. For
example, if you want to know the current value of 1 dollar in any given
currency, this function provides the latest exchange rate.

\### 2. Historical Function The \'historical\' function allows you to
retrieve exchange rates for any given date. For instance, if you want to
determine the value of 1 dollar in a specific currency for a date within
the range provided by the Open Exchange Rates API, you can do so, with
the available data extending back to January 1, 1999.

\### 3. Currencies Function The \'currencies\' function displays a list
of all currency symbols available from the Open Exchange Rates API,
along with their corresponding full names.

\### 4. Blackmarket Function The \'blackmarket\' function provides a
list of unofficial, black market, and alternative digital currencies.


# test_project.py

# Main Function
The main function calls the test functions for `latest`, `historical`, `currencies`, and `blackmarket`.

## test_latest Function
Tests the `latest` function with two cases: `latest("cat")` and `latest("dog")`.
Please note that I have included only two tests because this function provides the latest update of the value of a currency,
and those values could be updated every few minutes or hours.
So, given the test `assert latest("GBP") == f"1 US Dollar equals 0.789869 GBP"`, pytest initially shows it as correct,
but after a few minutes of retesting, the result may be incorrect.

## test_historical Function
Tests the `historical` function with three different dates and currencies.

## test_currencies Function
Tests the `currencies` function.
Checks if the result is a list.
Verifies whether it contains specific elements indicating success or an error.

## test_blackmarket Function
Tests the `blackmarket` function.
Similar to the `test_currencies` function, checks if the result is a list.
Verifies the contents of the list.

## \_\_main\_\_ Block
If the script is executed directly (not imported as a module).
Calls the main function to run all the tests.

