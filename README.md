import requests
import re
import time
import sys

def main():

    while True:
        print("Select an option:")
        print("1. latest")
        print("2. historical")
        print("3. currencies")
        print("4. blackmarket")
        print("ctrl D to Exit")

        try:
            choice = input("Enter the number of your choice: ")

            if choice == '1':  #latest
                iso = input("Please enter a valid currency code (e.g., EUR, GBP): ").upper()
                latest(iso)

            elif choice == '2':  #historical
                try:
                    iso = input("Please enter a valid currency code (e.g., EUR, GBP): ").upper()
                    if not re.match(r'^[A-Z]{3}$', iso):
                        print("Invalid currency code. Please enter a valid code such as USD, EUR, GBP, etc.")
                        continue

                    date = input("Please enter a date in the format YYYY-MM-DD: ")
                    if not re.match(r"\d{4}-\d{2}-\d{2}", date):
                        print("Invalid date format. Please enter the date in the format YYYY-MM-DD.")
                        continue
                    year = int(date.split('-')[0])
                    if year < 1999:
                            print("Date cannot be earlier than 1st January 1999")
                            continue
                except KeyError:
                    print("Invalid currency code. Please enter a valid code such as EUR, GBP, etc.")
                    continue
                historical(iso, date)

            elif choice == '3':
                currencies()
            elif choice == '4':
                blackmarket()
            else:
                print("Invalid choice. Please enter a valid option.")
        except EOFError:
            sys.exit("Program closed")



def latest(iso):
    url = 'https://openexchangerates.org/api/latest.json'
    app_id = '29b77fe9ac284e96b7e9bc656408d7a0'
    params = {'app_id': app_id}
    response = requests.get(url, params=params)
    exchange_rate = None

    try:
        if response.status_code == 200:
            data = response.json()
            exchange_rate = data['rates'][f'{iso}']
            print(f"1 US Dollar equals {exchange_rate} {iso}")

        else:
            print(f"Error: {response.status_code}")
        time.sleep(4)
    except KeyError:
        print("Invalid input")
        time.sleep(2)
        return "Invalid input"
    return f"1 US Dollar equals {exchange_rate} {iso}"

def historical(iso, date):
    app_id = '29b77fe9ac284e96b7e9bc656408d7a0'
    oxr_url = f"https://openexchangerates.org/api/historical/{date}.json"
    params = {'app_id': app_id}

    response = requests.get(oxr_url, params=params)
    data = response.json()
    print(f"On {date}, 1 US Dollar was worth {data['rates'][iso]} {iso}")
    time.sleep(4)
    return f"On {date}, 1 US Dollar was worth {data['rates'][iso]} {iso}"


def currencies():
    url = 'https://openexchangerates.org/api/currencies.json?show_alternative=1'
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        currency_list = []
        for currency_code, currency_symbol in data.items():
            print(f"Currency Code: {currency_code}, Symbol: {currency_symbol}")
            currency_list.append(f"Currency Code: {currency_code}, Symbol: {currency_symbol}")
        time.sleep(2)
        return currency_list
    else:
        print(f"Error: {response.status_code}")
    time.sleep(4)

def blackmarket():
    url = 'https://openexchangerates.org/api/currencies.json?only_alternative=1'
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        bm_list = []
        for currency_code, currency_name in data.items():
            print(f"Currency Code: {currency_code}, Currency Name: {currency_name}")
            bm_list.append(f"Currency Code: {currency_code}, Currency Name: {currency_name}")
        time.sleep(2)
        return bm_list
    else:
        print(f"Error: {response.status_code}")
    time.sleep(4)

if __name__ == "__main__":
    main()
