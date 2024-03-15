#include <iostream>
#include <string>

using namespace std;

// Structure for Customer
struct Customer {
    int customerID;
    string customerName;
    string phoneNumber;
    string address;
    double balance;
    Customer* next;
};

// Class for Linked List
class CustomerList {
private:
    Customer* head;

public:
    CustomerList() : head(nullptr) {}

    // Function to insert a new customer at the beginning of the list
    void insertCustomer(int id, string name, string phone, string addr, double bal) {
        Customer* newCustomer = new Customer;
        newCustomer->customerID = id;
        newCustomer->customerName = name;
        newCustomer->phoneNumber = phone;
        newCustomer->address = addr;
        newCustomer->balance = bal;
        newCustomer->next = head;
        head = newCustomer;
    }

    // Function to search for a customer by ID
    Customer* searchCustomerByID(int id) {
        Customer* current = head;
        while (current != nullptr) {
            if (current->customerID == id)
                return current;
            current = current->next;
        }
        return nullptr; // Customer not found
    }

    // Function to display all customers in the list
    void displayCustomers() {
        Customer* current = head;
        cout << "Customer List:\n";
        while (current != nullptr) {
            cout << "ID: " << current->customerID << ", Name: " << current->customerName
                 << ", Phone: " << current->phoneNumber << ", Address: " << current->address
                 << ", Balance: $" << current->balance << endl;
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    // Array of structures
    const int MAX_CUSTOMERS = 5;
    Customer customersArray[MAX_CUSTOMERS] = {
        {101, "John Doe", "123-456-7890", "123 Main St", 100.0},
        {102, "Jane Smith", "456-789-0123", "456 Elm St", 150.0},
        {103, "Alice Johnson", "789-012-3456", "789 Oak St", 200.0},
        {104, "Bob Williams", "987-654-3210", "987 Pine St", 50.0},
        {105, "Eve Brown", "321-654-9870", "321 Maple St", 300.0}
    };

    // Linked list of structures
    CustomerList customerLinkedList;
    for (int i = 0; i < MAX_CUSTOMERS; ++i) {
        customerLinkedList.insertCustomer(customersArray[i].customerID, customersArray[i].customerName,
                                           customersArray[i].phoneNumber, customersArray[i].address,
                                           customersArray[i].balance);
    }

    // Searching for a customer by ID
    int searchID;
    cout << "Enter customer ID to search: ";
    cin >> searchID;
    Customer* foundCustomer = customerLinkedList.searchCustomerByID(searchID);
    if (foundCustomer != nullptr) {
        cout << "Customer found:\n";
        cout << "ID: " << foundCustomer->customerID << ", Name: " << foundCustomer->customerName
             << ", Phone: " << foundCustomer->phoneNumber << ", Address: " << foundCustomer->address
             << ", Balance: $" << foundCustomer->balance << endl;
    } else {
        cout << "Customer with ID " << searchID << " not found.\n";
    }

    return 0;
}
