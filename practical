from abc import ABC, abstractmethod


# Abstract Base Class

class HotelItem(ABC):
    def __init__(self, item_id, name, base_price, capacity):
        self.__item_id = item_id
        self.__name = name
        self.set_base_price(base_price)
        self.set_capacity(capacity)

    # ---------- Getters ----------
    def get_item_id(self):
        return self.__item_id

    def get_name(self):
        return self.__name

    def get_base_price(self):
        return self.__base_price

    def get_capacity(self):
        return self.__capacity

    # ---------- Setters with Validation ----------
    def set_base_price(self, price):
        if price <= 0:
            raise ValueError("Price must be positive.")
        self.__base_price = price

    def set_capacity(self, capacity):
        if capacity <= 0:
            raise ValueError("Capacity must be greater than 0.")
        self.__capacity = capacity

    # ---------- Abstract Methods ----------
    @abstractmethod
    def calculate_item_cost(self):
        pass

    @abstractmethod
    def display_details(self):
        pass



# Hotel Room Class

class HotelRoom(HotelItem):
    CITY_TAX = 0.15

    def __init__(self, item_id, name, base_price, capacity, bed_size, smoking_allowed):
        super().__init__(item_id, name, base_price, capacity)
        self.__bed_size = bed_size
        self.__smoking_allowed = smoking_allowed

    def get_bed_size(self):
        return self.__bed_size

    def is_smoking_allowed(self):
        return self.__smoking_allowed

    def calculate_item_cost(self):
        return self.get_base_price() * (1 + HotelRoom.CITY_TAX)

    def display_details(self):
        smoking = "Yes" if self.__smoking_allowed else "No"
        print(f"""
[Room] {self.get_name()}
ID: {self.get_item_id()}
Price Per Night: ${self.get_base_price():.2f}
Capacity: {self.get_capacity()} guest(s)
Bed Size: {self.__bed_size}
Smoking Allowed: {smoking}
""")



# Spa Service Class

class SpaService(HotelItem):
    GRATUITY = 0.20

    def __init__(self, item_id, name, base_price, capacity, duration_minutes):
        super().__init__(item_id, name, base_price, capacity)
        self.__duration_minutes = duration_minutes

    def get_duration(self):
        return self.__duration_minutes

    def calculate_item_cost(self):
        return self.get_base_price() * (1 + SpaService.GRATUITY)

    def display_details(self):
        print(f"""
[Service] {self.get_name()}
ID: {self.get_item_id()}
Service Fee: ${self.get_base_price():.2f}
Capacity: {self.get_capacity()} person(s)
Duration: {self.__duration_minutes} minutes
""")



# Customer Reservation

class CustomerReservation:
    def __init__(self, customer_name):
        self.customer_name = customer_name
        self.reserved_items = []

    def add_item(self, item):
        self.reserved_items.append(item)
        print(f"'{item.get_name()}' added successfully.\n")

    def view_reservation(self):
        if not self.reserved_items:
            print("Reservation is currently empty.\n")
            return

        print("\n===== CURRENT RESERVATION =====")
        for item in self.reserved_items:
            print(f"- {item.get_name()} (${item.get_base_price():.2f})")
        print()

    def print_final_folio(self):
        if not self.reserved_items:
            print("No items in reservation.\n")
            return

        print("\n========== HOTEL FINAL FOLIO ==========")
        print(f"Guest Name: {self.customer_name}")
        print("---------------------------------------")

        total = 0

        for item in self.reserved_items:
            item_total = item.calculate_item_cost()
            total += item_total

            print(f"{item.get_name():25} ${item_total:.2f}")

        print("---------------------------------------")
        print(f"TOTAL AMOUNT DUE:        ${total:.2f}")
        print("=======================================\n")



# Hotel Offerings

hotel_items = [
    HotelRoom("R101", "Deluxe King Room", 200, 2, "King", False),
    HotelRoom("R102", "Twin Standard Room", 150, 2, "Twin", True),
    SpaService("S201", "Relaxation Massage", 80, 1, 60),
    SpaService("S202", "Luxury Facial", 120, 1, 90)
]



# Helper Functions

def display_all_items():
    print("\n======= AVAILABLE HOTEL OFFERINGS =======")

    for item in hotel_items:
        item.display_details()

    print("=========================================\n")


def find_item(search_value):
    for item in hotel_items:
        if (
            item.get_item_id().lower() == search_value.lower()
            or item.get_name().lower() == search_value.lower()
        ):
            return item
    return None



# Main Program

def main():
    print("====================================")
    print(" Welcome to Smart Hotel Booking ")
    print("====================================")

    customer_name = input("Enter customer name: ")
    reservation = CustomerReservation(customer_name)

    while True:
        print("""
========= MAIN MENU =========
1. View Hotel Offerings
2. Add Item to Reservation
3. View Current Reservation
4. Print Final Bill
5. Exit
=============================
""")

        choice = input("Enter your choice: ")

        try:
            choice = int(choice)

            if choice == 1:
                display_all_items()

            elif choice == 2:
                search = input("Enter Item ID or Name: ")
                item = find_item(search)

                if item:
                    reservation.add_item(item)
                else:
                    print("Item not found.\n")

            elif choice == 3:
                reservation.view_reservation()

            elif choice == 4:
                reservation.print_final_folio()

            elif choice == 5:
                print("Thank you for using Smart Hotel Booking System.")
                print("Goodbye!")
                break

            else:
                print("Invalid menu choice. Please try again.\n")

        except ValueError:
            print("Invalid input. Please enter a valid number.\n")



# Run Program

if __name__ == "__main__":
    main()