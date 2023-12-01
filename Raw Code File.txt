# ---------------------------------------------------------------------------------------------------------------------
# I have implemented the basic functionality required by the assignment. However, the  bonus AWS
# section has been intentionally skipped by me since I do not have the proper AWS S3 credentials
# to upload the JSON files there. I could have used the 'boto' library to implement the added functionality
# --------------------------------------------------------------------------------------------------- #


class ParkingLot:
    def __init__(self, square_footage):  # Magic Method
        # Calculate the number of parking spots based on the square footage
        self.parking_spots = [False] * (square_footage // 96)  # Assuming each spot is 8x12 (96 ft2)

    def find_available_spot(self):
        for i, occupied in enumerate(self.parking_spots):
            if not occupied:
                return i
        return -1  # No available spot

    def park_car(self, spot):
        if spot < 0 or spot >= len(self.parking_spots):
            return False  # Invalid spot
        if self.parking_spots[spot]:
            return False  # Spot is already occupied

        self.parking_spots[spot] = True
        return True  # Car parked successfully


class Car:
    def __init__(self, license_plate):  # Magic Method
        self.license_plate = license_plate

    def __str__(self):  # Magic Method
        return self.license_plate

    def park(self, parking_lot, spot):
        return parking_lot.park_car(spot)


def main():
    parking_lot = ParkingLot(2000)  # Create a parking lot of size 2000ft2

    #  Creating a list of cars with random license plates
    cars = [
        Car("ABC1234"),
        Car("XYZ5678"),
        Car("DEF9876"),
        # ... We can add more cars as needed
    ]

    for car in cars:
        available_spot = parking_lot.find_available_spot()
        if available_spot != -1:
            car.park(parking_lot, available_spot)
            print(f"Car with license plate {car} parked successfully in spot {available_spot}")
        else:
            print("Parking lot is full. Exiting program.")
            break


if __name__ == "__main__":
    main()
