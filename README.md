
CREATE DATABASE Uber;
USE Uber;
CREATE TABLE Drivers (
    driver_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    phone VARCHAR(15),
    license_no VARCHAR(20),
    city VARCHAR(30));
INSERT INTO Drivers (name, phone, license_no, city) VALUES
('Arun Kumar', '9876543210', 'LIC12345', 'Chennai'),
('Ravi Raj', '9876543211', 'LIC12346', 'Bangalore'),
('Mohan Das', '9876543212', 'LIC12347', 'Hyderabad'),
('Siva Kumar', '9876543213', 'LIC12348', 'Mumbai'),
('Vijay Anand', '9876543214', 'LIC12349', 'Delhi'),
('Karthik', '9876543215', 'LIC12350', 'Pune'),
('Suresh', '9876543216', 'LIC12351', 'Kolkata'),
('Manoj', '9876543217', 'LIC12352', 'Chennai'),
('Anand', '9876543218', 'LIC12353', 'Bangalore'),
('Rahul', '9876543219', 'LIC12354', 'Hyderabad');
CREATE TABLE Riders (
    rider_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    phone VARCHAR(15),
    email VARCHAR(50),
    city VARCHAR(30));
INSERT INTO Riders (name, phone, email, city) VALUES
('Balaji', '9000000001', 'balaji@mail.com', 'Chennai'),
('Lakshmi', '9000000002', 'lakshmi@mail.com', 'Bangalore'),
('Ramya', '9000000003', 'ramya@mail.com', 'Hyderabad'),
('Naveen', '9000000004', 'naveen@mail.com', 'Mumbai'),
('Priya', '9000000005', 'priya@mail.com', 'Delhi'),
('Kiran', '9000000006', 'kiran@mail.com', 'Pune'),
('Deepa', '9000000007', 'deepa@mail.com', 'Kolkata'),
('Sathish', '9000000008', 'sathish@mail.com', 'Chennai'),
('Gokul', '9000000009', 'gokul@mail.com', 'Bangalore'),
('Meena', '9000000010', 'meena@mail.com', 'Hyderabad');
CREATE TABLE Vehicles (
    vehicle_id INT PRIMARY KEY AUTO_INCREMENT,
    driver_id INT,
    model VARCHAR(50),
    plate_no VARCHAR(20),
    type VARCHAR(20),
    FOREIGN KEY (driver_id) REFERENCES Drivers(driver_id));
INSERT INTO Vehicles (driver_id, model, plate_no, type) VALUES
(1, 'Honda City', 'TN01AB1234', 'Car'),
(2, 'Suzuki WagonR', 'KA05CD5678', 'Car'),
(3, 'Hyundai i20', 'TS09EF3456', 'Car'),
(4, 'Toyota Innova', 'MH12GH7890', 'Car'),
(5, 'Bajaj RE', 'DL04IJ1122', 'Auto'),
(6, 'Kia Seltos', 'MH14KL3344', 'Car'),
(7, 'Maruti Swift', 'WB20MN5566', 'Car'),
(8, 'Hyundai Verna', 'TN10OP7788', 'Car'),
(9, 'Ola Electric S1', 'KA07QR9900', 'Bike'),
(10, 'TVS iQube', 'TS11ST2233', 'Bike');
CREATE TABLE Trips (
    trip_id INT PRIMARY KEY AUTO_INCREMENT,
    rider_id INT,
    driver_id INT,
    pickup VARCHAR(50),
    drop_loc VARCHAR(50),
    fare DECIMAL(6,2),
    status VARCHAR(20),
    FOREIGN KEY (rider_id) REFERENCES Riders(rider_id),
    FOREIGN KEY (driver_id) REFERENCES Drivers(driver_id));
INSERT INTO Trips (rider_id, driver_id, pickup, drop_loc, fare, status) VALUES
(1, 1, 'Chennai Central', 'T Nagar', 250.00, 'Completed'),
(2, 2, 'MG Road', 'Indiranagar', 180.00, 'Completed'),
(3, 3, 'HiTech City', 'Gachibowli', 200.00, 'Completed'),
(4, 4, 'Andheri', 'Bandra', 300.00, 'Completed'),
(5, 5, 'Connaught Place', 'Karol Bagh', 150.00, 'Cancelled'),
(6, 6, 'Shivaji Nagar', 'Hinjewadi', 220.00, 'Completed'),
(7, 7, 'Howrah', 'Salt Lake', 280.00, 'Completed'),
(8, 8, 'Velachery', 'OMR', 190.00, 'Completed'),
(9, 9, 'Whitefield', 'Marathahalli', 210.00, 'Ongoing'),
(10, 10, 'Secunderabad', 'Madhapur', 230.00, 'Completed');
CREATE TABLE Payments (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    trip_id INT,
    amount DECIMAL(6,2),
    method VARCHAR(20),
    status VARCHAR(20),
    FOREIGN KEY (trip_id) REFERENCES Trips(trip_id));
INSERT INTO Payments (trip_id, amount, method, status) VALUES
(1, 250.00, 'UPI', 'Success'),
(2, 180.00, 'Cash', 'Success'),
(3, 200.00, 'Card', 'Success'),
(4, 300.00, 'UPI', 'Success'),
(5, 0.00, 'None', 'Cancelled'),
(6, 220.00, 'Cash', 'Success'),
(7, 280.00, 'Card', 'Success'),
(8, 190.00, 'UPI', 'Success'),
(9, 210.00, 'UPI', 'Pending'),
(10, 230.00, 'Cash', 'Success');
CREATE TABLE Ratings (
    rating_id INT PRIMARY KEY AUTO_INCREMENT,
    trip_id INT,
    rider_id INT,
    driver_id INT,
    stars INT,
    comment VARCHAR(100),
    FOREIGN KEY (trip_id) REFERENCES Trips(trip_id),
    FOREIGN KEY (rider_id) REFERENCES Riders(rider_id),
    FOREIGN KEY (driver_id) REFERENCES Drivers(driver_id));
INSERT INTO Ratings (trip_id, rider_id, driver_id, stars, comment) VALUES
(1, 1, 1, 5, 'Excellent ride'),
(2, 2, 2, 4, 'Good service'),
(3, 3, 3, 5, 'Very smooth trip'),
(4, 4, 4, 3, 'Driver was late'),
(5, 5, 5, 0, 'Cancelled'),
(6, 6, 6, 4, 'Clean car'),
(7, 7, 7, 5, 'Very friendly driver'),
(8, 8, 8, 4, 'Nice experience'),
(9, 9, 9, 3, 'Ride still ongoing'),
(10, 10, 10, 5, 'Perfect trip');
# SQL-Database-Uber
