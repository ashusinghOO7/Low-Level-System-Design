Parking Lot Low Level System Design


Questions to ask 

-> Number of Entries, Floors.
-> Type of Vehicles
-> Are there different type of parking spots for different vehicles


Functional Requirement

-> User should park the vehicle finding the available spot
-> User can unpark the vehicle and free up the available spot
-> Find nearest available slot available
-> Show available parking spot count vehicle wise
-> Payment calculation based on duration, type of vehicle

Non Functional Requirement

-> Optimization for fast parking/unparking.
-> Extensible for new vehicle type or new Parking strategy.


Core Classes and Objects


-> Parking Lot  -  Main Class i.e. defines the whole Parking Lot
-> Floors (If multiple floors are there)  -  Represents a single floor 
-> Parking Spot   -   Represent an individual parking spot to park the vehicle
-> Vehicle  -   Represent the vehicle to be parked
-> Ticket  -  Represent the parking ticket that is issued to the vehicle
-> Payment -  Handles Payment processing
-> Parking Strategy   -   Decides how to assign parking strategy (i.e. Nearest to entrance)


Design Pattern 

    To make the system robust and maintainable, I’ll use the following design patterns:

	Singleton Pattern:
	-> I will use this for the ParkingLot class to ensure there’s only one instance of the parking lot system.

	Factory Pattern:
	-> I will use this to create different types of Vehicle objects (e.g., car, bike, truck).

	Strategy Pattern:
	-> I will use this to implement different parking strategies (e.g., nearest spot first, random spot).

	Observer Pattern:
	-> I will use this to notify the system when a parking spot becomes available or occupied.

	State Pattern:
	-> I will use this to manage the state of a ParkingSpot (e.g., available, occupied, under maintenance).

	Decorator Pattern:
	-> I will use this for the price calculation. (i.e. Fixed charge for initial hour and then x amount for each hour)


Class Diagram
	
	-> Parking Lot
		floors : List<Floor>;

		assignSpot(Vehicle vehicle) : Ticket;
		freeSpot(Ticket ticket) : void

	-> Floor
		parkingSpots : List<ParkingSpot>;

		findParkingSpot(vehicleType : VehicleType) : ParkingSpot;

	-> Parking Spot
		spotId : String;
		spotType : Enum <VehicleType> ;
		state : ParkingSpotState;

		isAvailable() : Boolean;

	-> Vehicle (Abstract)
		licenseNumber : String;
		
		getType() : Enum <VehicleType>;
			NOTE - Concrete Class will be based on requirement (i.e. Car, Truck, Motorcycle  or  compactVehicle, normalVehicle, largeVehicle)
	
	-> Ticket
		ticketId : String;
		entryTime : DateTime;
		spot : ParkingSpot;
		vehicle : Vehicle;

	-> Payment (Interface)
		calculateFee(Ticket ticket) : double;

	-> Base Payment (Concrete Class) 
		calculateFee(Ticket ticket) : double;

	-> VehicleTypeDecorator (Abstract Decorator)
   		payment: Payment

		calculateFee(ticket: Ticket): double

	-> CarPaymentDecorator, BikePaymentDecorator, TruckPaymentDecorator (Concrete Decorators)
   		calculateFee(ticket: Ticket): double
		
		


		
		
		
