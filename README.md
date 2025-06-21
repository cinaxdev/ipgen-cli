# Copyright (c) 2025 Cinax
# This software is licensed under the MIT License.
# Permission is granted to use, copy, modify, and distribute this software,
# provided that the above copyright notice and this license appear in all copies.

import ipaddress
import random

country_ip_blocks = {
    "Turkey": [
        "185.82.0.0/16",
        "91.213.96.0/19",
        "31.210.0.0/16",
        "176.53.0.0/17",
        "193.140.0.0/15",
        "89.19.0.0/16"
    ],
    "UK": [
        "212.58.224.0/19",
        "86.128.0.0/10",
        "51.140.0.0/14",
        "79.72.0.0/13"
    ],
    "USA": [
        "8.8.8.0/24",
        "66.249.64.0/19",
        "3.0.0.0/8",
        "23.0.0.0/8",
        "52.0.0.0/8"
    ]
}

def random_ip_from_cidr(cidr):
    network = ipaddress.IPv4Network(cidr)
    hosts = list(network.hosts())
    return str(random.choice(hosts))

def generate_ips_from_blocks(blocks, count=10):
    ips = []
    for _ in range(count):
        block = random.choice(blocks)
        ip = random_ip_from_cidr(block)
        ips.append(ip)
    return ips

def select_country():
    print("Select a country:")
    for i, country in enumerate(country_ip_blocks.keys(), start=1):
        print(f"{country}: {i}")
    while True:
        choice = input("Enter the number of the country: ").strip()
        if choice in ["1", "2", "3"]:
            return list(country_ip_blocks.keys())[int(choice)-1]
        else:
            print("Invalid choice, please select 1, 2, or 3.")

def main():
    print("Random realistic IP generator by country")
    print("----------------------------------------")
    while True:
        country = select_country()
        print(f"\nGenerating 10 random IPs for {country}...\n")
        blocks = country_ip_blocks[country]
        ips = generate_ips_from_blocks(blocks)
        for ip in ips:
            print(ip)
        answer = input("\nGenerate again? (y/n): ").strip().lower()
        if answer != "y":
            print("Exiting program...")
            break
        print("\n----------------------------------------")

if __name__ == "__main__":
    main()
