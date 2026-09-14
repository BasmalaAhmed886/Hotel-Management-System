#include <bits/stdc++.h>
using namespace std;
bool getValidInt(int& num)
{
    if(cin.fail())
    {
        cin.clear();
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        return false;
    }
    return true;
}
// 1 Guest
class Guest
{
private:
    int id;
    string name;
    string phone;
    string email;
    string address;
    string checkInDate;
    string checkOutDate;
    bool checkedIn;

public:

    Guest(int id, string name, string phone, string email, string address)
    {
        this->id = id;
        this->name = name;
        this->phone = phone;
        this->email = email;
        this->address = address;

        checkedIn = false;
    }

    int getId()
    {
        return id;
    }

    string getName()
    {
        return name;
    }

    string getCheckInDate()
    {
        return checkInDate;
    }

    string getCheckOutDate()
    {
        return checkOutDate;
    }

    bool isCheckedIn()
    {
        return checkedIn;
    }

    void editData()
    {
        cout << "\nEnter new name: ";
        cin >> name;

        cout << "Enter new phone: ";
        cin >> phone;

        cout << "Enter new email: ";
        cin >> email;

        cout << "Enter new address: ";
        cin >> address;

        cout << "Guest data updated successfully!\n";
    }

    void checkIn(string date)
    {
        if (checkedIn)
        {
            cout << "Guest is already checked in!\n";
            return;
        }

        checkInDate = date;
        checkedIn = true;

        cout << "Check-in completed successfully!\n";
    }

    void checkOut(string date)
    {
        if (!checkedIn)
        {
            cout << "Guest is not checked in!\n";
            return;
        }

        checkOutDate = date;
        checkedIn = false;

        cout << "Check-out completed successfully!\n";
    }

    void displayGuest()
    {
        cout << "\nID: " << id << endl;
        cout << "Name: " << name << endl;
        cout << "Phone: " << phone << endl;
        cout << "Email: " << email << endl;
        cout << "Address: " << address << endl;
        cout << "Check-in Date: " << (checkInDate.empty() ? "N/A" : checkInDate) << endl;
        cout << "Check-out Date: " << (checkOutDate.empty() ? "N/A" : checkOutDate) << endl;
        cout << "Status: " << (checkedIn ? "Checked In" : "Not Checked In") << endl;

        cout << "============================\n";
    }
};

class GuestManager
{
private:
    vector<shared_ptr<Guest>> guests;

public:

    void addGuest()
    {
        int id;
        string name, phone, email, address;
        cout << "\nEnter Guest ID: ";
        cin >> id;

        if(!getValidInt(id))
        {
            cout << "\n== Invalid input! Please enter numbers only ==\n";
            return;
        }

        if(getGuest(id) != nullptr)
        {
            cout << "Guest ID already exists!\n";
            return;
        }

        cout << "Enter Name: ";
        cin.ignore();
        getline(cin, name);

        cout << "Enter Phone: ";
        cin >> phone;
        bool valid = true;
        for(char c : phone)
        {
            if(!isdigit(c))
            {
                valid = false;
                break;
            }
        }
        if(!valid)
        {
            cout << "Invalid phone number! Please enter numbers only\n";
            return;
        }

        cout << "Enter Email: ";
        cin >> email;

        cout << "Enter Address: ";
        cin.ignore();
        getline(cin, address);

        auto guest = make_shared<Guest>( id, name, phone, email, address );
        guests.push_back(guest);
        cout << "Guest added successfully!\n";
    }

    shared_ptr<Guest> getGuest(int id)
    {
        for (auto guest : guests)
        {
            if (guest->getId() == id)
                return guest;
        }

        return nullptr;
    }

    void displayAllGuests()
    {
        if (guests.empty())
        {
            cout << "No guests found!\n";
            return;
        }

        cout << "\n============================\n";
        cout << "        GUEST DETAILS\n";
        cout << "============================\n";

        for (auto guest : guests)
        {
            guest->displayGuest();
        }
    }
};

// 2 Room
class Room
{
protected:
    int roomNumber;
    double price;
    bool available;
public:
    Room(int number, double p)
    {
        roomNumber = number;
        price = p;
        available = true;
    }
    virtual string getType() = 0;

    int getRoomNumber()
    {
        return roomNumber;
    }
    double getPrice()
    {
        return price;
    }
    double getSeasonPrice(int choice)
    {
        if (choice == 1)
        {
            return price * 1.3;
        }
        else if(choice == 3)
        {
            return price*0.7;
        }
        return price;
    }
    bool isAvailable()
    {
        return available;
    }

    bool bookRoom()
    {
        if (available)
        {
            available = false;
            cout << "Room booked successfully^~^\n";
            return true;
        }
        else
        {
            cout << "Room is already booked!\n";
            return false;
        }
    }

    void cancelBooking()
    {
        if (!available)
        {
            available = true;
            cout << "Booking canceled successfully^~^\n";
        }
        else
        {
            cout << "Room is already available!\n";
        }
    }

    void displayRoom(int seasonChoice)
    {
        cout << "\nRoom Number: " << roomNumber << endl;
        cout << "Type: " << getType() << endl;
        cout << "Price: " << getSeasonPrice(seasonChoice) << endl;
        cout << "Status: " << (available ? "Available" : "Booked") << endl;
    }
};

class SingleRoom : public Room
{
public:

    SingleRoom(int number, double price) : Room(number, price) {}
    string getType() override
    {
        return "Single";
    }
};
class DoubleRoom : public Room
{
public:

    DoubleRoom(int number, double price) : Room(number, price) {}
    string getType() override
    {
        return "Double";
    }
};
class SuiteRoom : public Room
{
public:

    SuiteRoom(int number, double price) : Room(number, price) {}
    string getType() override
    {
        return "Suite";
    }
};
class ConferenceRoom : public Room
{
public:

    ConferenceRoom(int number, double price) : Room(number, price) {}
    string getType() override
    {
        return "Conference";
    }
};

class Booking
{
private:
    shared_ptr<Guest> guest;
    shared_ptr<Room> room;

public:

    Booking(shared_ptr<Guest> g, shared_ptr<Room> r)
    {
        guest = g;
        room = r;
    }

    shared_ptr<Guest> getGuest()
    {
        return guest;
    }

    shared_ptr<Room> getRoom()
    {
        return room;
    }
};

class BookingManager
{
private:
    vector<shared_ptr<Room>> rooms;
    vector<shared_ptr<Booking>> bookings;

public:
    void addRoom(shared_ptr<Room> room)
    {
        rooms.push_back(room);
    }

    shared_ptr<Room> findRoom(int number)
    {
        for (auto room : rooms)
        {
            if (room->getRoomNumber() == number)
                return room;
        }

        return nullptr;
    }

    void displayAvailableRooms()
    {
        int seasonChoice;
        cout << "\n===== AVAILABLE ROOMS =====\n";
        cout << "1.High season\n2.Normal season\n3.Low season\n";
        cout << "\n=> Enter season: ";
        cin >> seasonChoice;

        if(cin.fail() || seasonChoice > 3 || seasonChoice < 1)
        {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "\n--| Invalid input! choice from 1 to 3 |--\n";
            return;
        }

        bool found = false;
        for (auto room : rooms)
        {
            if (room->isAvailable())
            {
                room->displayRoom(seasonChoice);
                found = true;
            }
        }

        if (!found)
            cout << "No available rooms!\n";
    }

    bool hasBooking(shared_ptr<Guest> guest)
    {
        for (auto booking : bookings)
        {
            if (booking->getGuest() == guest)
                return true;
        }

        return false;
    }

    shared_ptr<Booking> findBooking(shared_ptr<Guest> guest)
    {
        for (auto booking : bookings)
        {
            if (booking->getGuest() == guest)
                return booking;
        }

        return nullptr;
    }

    void bookRoom(shared_ptr<Guest> guest)
    {
        if (hasBooking(guest))
        {
            cout << "Guest already has a booking!\n";
            return;
        }

        int number;
        cout << "Enter room number: ";
        cin >> number;

        if(!getValidInt(number))
        {
            cout << "\n== Invalid input! Please enter numbers only ==\n";
            return;
        }

        auto room = findRoom(number);
        if (room == nullptr)
        {
            cout << "Room not found!\n";
            return;
        }
        if (!room->isAvailable())
        {
            cout << "Room is already booked!\n";
            return;
        }

        if (room->bookRoom())
        {
            auto booking = make_shared<Booking>(guest, room);
            bookings.push_back(booking);
        }
    }

    void cancelBooking(shared_ptr<Guest> guest)
    {
        auto booking = findBooking(guest);
        if (booking == nullptr)
        {
            cout << "Guest has no booking!\n";
            return;
        }
        auto room = booking-> getRoom();
        room->cancelBooking();
        bookings.erase(remove(bookings.begin(), bookings.end(), booking), bookings.end());
        }

    void checkInGuest(shared_ptr<Guest> guest)
    {
        auto booking = findBooking(guest);

        if (booking == nullptr)
        {
            cout << "Guest has no booking!\n";
            return;
        }

        if (guest->isCheckedIn())
        {
            cout << "Guest is already checked in!\n";
            return;
        }

        string date;
        cout << "Enter Check-in Date: ";
        cin >> date;
        guest->checkIn(date);
    }

    void checkOutGuest(shared_ptr<Guest> guest)
    {
        auto booking = findBooking(guest);

        if (booking == nullptr)
        {
            cout << "Guest has no booking!\n";
            return;
        }
        if (!guest->isCheckedIn())
        {
            cout << "Guest is not checked in!\n";
            return;
        }
        string date;
        cout << "Enter Check-out Date: ";
        cin >> date;
        guest->checkOut(date);
        booking->getRoom()->cancelBooking();

        // Remove booking
        for (auto it = bookings.begin();
                it != bookings.end(); ++it)
        {
            if ((*it)->getGuest() == guest)
            {
                bookings.erase(it);
                break;
            }
        }

        cout << "Room is now available.\n";
    }

};
// 3 Service
class Service
{
private:
    string name;
    double price;

public:

    Service(string n, double p)
    {
        name = n;
        price = p;
    }

    string getName()
    {
        return name;
    }

    double getPrice()
    {
        return price;
    }
};

class Billing
{
private:
    shared_ptr<Guest> guest;
    shared_ptr<Room> room;

    int days;
    string season;

    vector<Service> services;

public:

    Billing(shared_ptr<Guest> g, shared_ptr<Room> r, int d, string s)
    {
        guest = g;
        room = r;
        days = d;
        season = s;
    }

    double getSeasonPrice()
    {
        double price = room->getPrice();
        for(char& c : season)
        {
            c = tolower(c);
        }
        if (season == "high")
        {
            return price * 1.3;
        }

        else if (season == "low")
        {
            return price * 0.7;
        }
        return price;
    }

    double roomCost()
    {
        return days * getSeasonPrice();
    }

    void addService(string name, double price)
    {
        services.push_back(Service(name, price));
    }

    double servicesCost()
    {
        double total = 0;

        for (auto service : services)
        {
            total += service.getPrice();
        }

        return total;
    }

    double total()
    {
        return roomCost() + servicesCost();
    }

    void showBill()
    {
        cout << "\n=================================\n";
        cout << "            HOTEL BILL\n";
        cout << "=================================\n";

        cout << "Guest: " << guest->getName() << endl;
        cout << "Room Number: " << room->getRoomNumber() << endl;
        cout << "Room Type: " << room->getType() << endl;
        cout << "Days: " << days << endl;
        cout << "Season: " << season << endl;
        cout << fixed << setprecision(2);
        cout << "Price Per Night: " << getSeasonPrice() << endl;
        cout << "Room Cost: " << roomCost() << endl;
        cout << "\nServices:\n";

        if (services.empty())
        {
            cout << "No services\n";
        }
        else
        {
            for (auto service : services)
            {
                cout << "- "
                     << service.getName()
                     << ": "
                     << service.getPrice()
                     << endl;
            }
        }

        cout << "Services Cost: " << servicesCost() << endl;
        cout << "---------------------------------\n";
        cout << "TOTAL: " << total() << endl;
        cout << "=================================\n";
    }
};

class HouseKeeping
{
private:
    int roomNumber;
    string status;

public:

    HouseKeeping(int room, string st)
    {
        roomNumber = room;
        status = st;
    }

    void display()
    {
        cout << "Room Number: " << roomNumber << endl;
        cout << "Status: " << status << endl;
    }

    void requestCleaning()
    {
        status = "Requested";
        cout << "Cleaning requested successfully!\n";
    }

    void completeCleaning()
    {
        status = "Complete";
        cout << "Cleaning completed successfully!\n";
    }
};

class Review
{
private:
    int rating;
    string comment;

public:

    void addReview()
    {
        int r;
        string c;
        cout << "Enter Rating (1-5): ";
        cin >> r;

        if(!getValidInt(r))
        {
            cout << "\n---| Invalid input! Please enter numbers only |---\n";
            return;
        }

        if(r > 5||r < 1)
        {
            cout << "Invalid value! Rating between 1 and 5.\n";
        }
        else
        {
            cout << "Enter Comment: ";
            cin.ignore();
            getline(cin, c);
            rating = r;
            comment = c;
            cout << "Thank you for your feedback ^~^\n";
        }
    }

    void displayReview()
    {
        cout << "\n======= HOTEL REVIEW =======\n";
        cout << "Rating: " << rating << endl;
        cout << "Comment: " << comment << endl;
    }

};

int main()
{
    GuestManager guestManager;
    BookingManager bookingManager;
    Review review;

    bookingManager.addRoom(make_shared<SingleRoom>(101, 500));
    bookingManager.addRoom(make_shared<DoubleRoom>(201, 800));
    bookingManager.addRoom(make_shared<SuiteRoom>(301, 1500));
    bookingManager.addRoom(make_shared<ConferenceRoom>(401, 2000));

    int choice;
    do
    {
        cout << "\n====================================\n";
        cout << "     = HOTEL MANAGEMENT SYSTEM =\n";
        cout << "====================================\n";

        cout << "1. Add Guest\n";
        cout << "2. Display Guests\n\n";
        cout << "3. Display Available Rooms\n";
        cout << "4. Book Room\n";
        cout << "5. Cancel Booking\n\n";
        cout << "6. Check-in\n";
        cout << "7. Check-out\n\n";
        cout << "8. Create Bill\n";
        cout << "9. HouseKeeping\n\n";
        cout << "10.Add Review\n";
        cout << "11.Display Reviews\n\n";

        cout << "0. Exit\n====================================\n";
        cout << "\nEnter choice: ";
        cin >> choice;

        switch(choice)
        {
        case 1:
        {
            guestManager.addGuest();
            break;
        }

        case 2:
        {
            guestManager.displayAllGuests();
            break;
        }

        case 3:
        {
            bookingManager.displayAvailableRooms();
            break;
        }

        case 4:
        {
            int guestID;

            cout << "Enter Guest ID: ";
            cin >> guestID;

            if(!getValidInt(guestID))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }
            auto guest = guestManager.getGuest(guestID);

            if (guest == nullptr)
            {
                cout << "Guest not found!\n";
            }
            else
            {
                bookingManager.bookRoom(guest);
            }
            break;
        }

        case 5:
        {
            int guestID;

            cout << "Enter Guest ID: ";
            cin >> guestID;

            if(!getValidInt(guestID))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            auto guest = guestManager.getGuest(guestID);

            if (guest == nullptr)
            {
                cout << "Guest not found!\n";
            }
            else
            {
                bookingManager.cancelBooking(guest);
            }
            break;
        }

        case 6:
        {
            int guestID;
            cout << "Enter Guest ID: ";
            cin >> guestID;

            if(!getValidInt(guestID))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            auto guest =
                guestManager.getGuest(guestID);

            if (guest == nullptr)
            {
                cout << "Guest not found!\n";
            }
            else
            {
                bookingManager.checkInGuest(guest);
            }
            break;
        }

        case 7:
        {
            int guestID;
            cout << "Enter Guest ID: ";
            cin >> guestID;

            if(!getValidInt(guestID))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            auto guest =
                guestManager.getGuest(guestID);

            if (guest == nullptr)
            {
                cout << "Guest not found!\n";
            }
            else
            {
                bookingManager.checkOutGuest(guest);
            }
            break;
        }

        case 8:
        {
            int guestID;
            int roomNumber;
            int days;
            string season;

            cout << "Enter Guest ID: ";
            cin >> guestID;

            if(!getValidInt(guestID))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            auto guest = guestManager.getGuest(guestID);

            if (guest == nullptr)
            {
                cout << "Guest not found!\n";
                continue;
            }

            cout << "Enter Room Number: ";
            cin >> roomNumber;

            if(!getValidInt(roomNumber))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            auto room = bookingManager.findRoom(roomNumber);

            if (room == nullptr)
            {
                cout << "Room not found!\n";
                continue;
            }

            cout << "Enter Season (high/low/normal): ";
            cin >> season;

            cout << "Enter Number of Days: ";
            cin >> days;
            if(days<1)
            {
                cout << "Invalid value! Please try again\n";
                continue;
            }

            Billing bill
            (
                guest,
                room,
                days,
                season
            );

            double price;

            cout << "Breakfast price (0 if none): ";
            cin >> price;

            if (price > 0)
                bill.addService("Breakfast", price);


            cout << "Spa price (0 if none): ";
            cin >> price;

            if (price > 0)
                bill.addService("Spa", price);


            cout << "Gym price (0 if none): ";
            cin >> price;

            if (price > 0)
                bill.addService("Gym", price);


            bill.showBill();
            break;
        }

        case 9:
        {
            int roomNumber;
            int cleaningChoice;

            cout << "Enter Room Number: ";
            cin >> roomNumber;

            if(!getValidInt(roomNumber))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            HouseKeeping houseKeeping(
                roomNumber,
                "Not Requested"
            );

            cout << "\n1. Request Cleaning\t";
            cout << "2. Complete Cleaning\n\n";
            cout << "Enter choice: ";
            cin >> cleaningChoice;

            if(!getValidInt(cleaningChoice))
            {
                cout << "\n---| Invalid input! Please enter numbers only |---\n";
                break;
            }

            if(cleaningChoice != 1 && cleaningChoice != 2)
            {
                cout << "\n---| Invalid input! Please enter 1 or 2 |---\n";
                break;
            }
            if (cleaningChoice == 1)
            {
                houseKeeping.requestCleaning();
            }
            else if (cleaningChoice == 2)
            {
                houseKeeping.completeCleaning();
            }

            houseKeeping.display();
            break;
        }

        case 10:
        {
            review.addReview();
            break;
        }

        case 11:
        {
            review.displayReview();
        }

        case 0:
        {
            cout << "Thank you!\n";
            break;
        }

        default:
        {
            cout << "Invalid choice!\n";
        }

        }
    }
    while (choice != 0);


    return 0;
}
