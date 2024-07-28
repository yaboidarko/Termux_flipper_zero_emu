import os
import requests
import scapy.all as scapy
import bluetooth
from geopy.geocoders import Nominatim
from termux import API

def install_dependencies():
    os.system("pkg install python -y")
    os.system("pkg install git -y")
    os.system("pip install requests")
    os.system("pip install scapy")
    os.system("pip install geopy")
    os.system("pkg install bluez -y")
    os.system("pkg install nmap -y")
    os.system("pkg install termux-api -y")

def wifi_scanner():
    os.system("ifconfig wlan0 down")
    os.system("iwconfig wlan0 mode monitor")
    os.system("ifconfig wlan0 up")

    def packet_handler(packet):
        if packet.haslayer(scapy.Dot11):
            if packet.type == 0 and packet.subtype == 8:
                print(f"SSID: {packet.info.decode()}")

    print("Scanning for Wi-Fi networks...")
    scapy.sniff(iface="wlan0", prn=packet_handler)

def bluetooth_scanner():
    print("Scanning for Bluetooth devices...")
    devices = bluetooth.discover_devices(duration=8, lookup_names=True, flush_cache=True, lookup_class=False)
    print(f"Found {len(devices)} devices.")
    for addr, name in devices:
        print(f"Device: {name}, Address: {addr}")

def nfc_reader():
    print("NFC Reader not implemented yet.")

def weather_info():
    city = input("Enter city name: ")
    api_key = "your_api_key"
    base_url = "http://api.openweathermap.org/data/2.5/weather?"
    complete_url = base_url + "q=" + city + "&appid=" + api_key
    response = requests.get(complete_url)
    data = response.json()

    if data["cod"] != "404":
        main = data["main"]
        weather = data["weather"][0]
        print(f"City: {city}")
        print(f"Temperature: {main['temp']}K")
        print(f"Weather: {weather['description']}")
    else:
        print("City not found")

def geolocation():
    location_data = requests.get('https://ipinfo.io').json()
    print(f"IP: {location_data['ip']}")
    print(f"City: {location_data['city']}")
    print(f"Region: {location_data['region']}")
    print(f"Country: {location_data['country']}")
    print(f"Location: {location_data['loc']}")

def main_menu():
    while True:
        print("\n--- Flipper Zero Emulator ---")
        print("1. Install Dependencies")
        print("2. Wi-Fi Scanner")
        print("3. Bluetooth Scanner")
        print("4. NFC Reader")
        print("5. Weather Information")
        print("6. Geolocation")
        print("7. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            install_dependencies()
        elif choice == '2':
            wifi_scanner()
        elif choice == '3':
            bluetooth_scanner()
        elif choice == '4':
            nfc_reader()
        elif choice == '5':
            weather_info()
        elif choice == '6':
            geolocation()
        elif choice == '7':
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main_menu()
