#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

bool login() {
    const int USER_COUNT = 4;
    string usernames[USER_COUNT] = {"moeez", "reyan", "basit", "hammad"};
    string passwords[USER_COUNT] = {"moeez4758", "reyan123", "basit4772", "hammad123"};

    string username, password;
    cout << endl << "=== Login System ===" << endl;
    cout << "Username: ";
    cin >> username;
    cout << "Password: ";
    cin >> password;

    for (int i = 0; i < USER_COUNT; i++) {
        if (username == usernames[i] && password == passwords[i]) {
            cout << endl << "Login successful! Welcome, " << username << "!" << endl;
            return true;
        }
    }

    cout << endl << "Invalid credentials. Try again." << endl;
    return false;
}

class FoodItem {
public:
    int id;
    string name;
    double price;
    FoodItem* next;

    FoodItem(int i, string n, double p) {
        id = i;
        name = n;
        price = p;
        next = nullptr;
    }
};

class Menu {
private:
    FoodItem* head;

public:
    Menu() { head = nullptr; }

    void sortById() {
        if (!head || !head->next) return;
        bool swapped;
        do {
            swapped = false;
            FoodItem* current = head;
            while (current->next) {
                if (current->id > current->next->id) {
                    swap(current->id, current->next->id);
                    swap(current->name, current->next->name);
                    swap(current->price, current->next->price);
                    swapped = true;
                }
                current = current->next;
            }
        } while (swapped);
    }

    void addItem(int id, string name, double price) {
        FoodItem* newItem = new FoodItem(id, name, price);
        if (!head) {
            head = newItem;
        } else {
            FoodItem* temp = head;
            while (temp->next)
                temp = temp->next;
            temp->next = newItem;
        }
        sortById();
    }

    void deleteItem(int id) {
        if (!head) return;
        if (head->id == id) {
            FoodItem* toDelete = head;
            head = head->next;
            delete toDelete;
            return;
        }
        FoodItem* current = head;
        while (current->next && current->next->id != id)
            current = current->next;
        if (current->next) {
            FoodItem* toDelete = current->next;
            current->next = toDelete->next;
            delete toDelete;
        }
    }

    void updateItem(int id, string newName, double newPrice) {
        FoodItem* temp = head;
        while (temp) {
            if (temp->id == id) {
                temp->name = newName;
                temp->price = newPrice;
                cout << "Item updated successfully." << endl;
                sortById();
                return;
            }
            temp = temp->next;
        }
        cout << "Item not found." << endl;
    }

    void displayMenu() {
        FoodItem* temp = head;
        cout << endl << "--- MENU ---" << endl;
        while (temp) {
            cout << "ID: " << temp->id << " | " << temp->name << " | Rs" << fixed << setprecision(2) << temp->price << endl;
            temp = temp->next;
        }
    }

    FoodItem* searchLinear(string name) {
        FoodItem* temp = head;
        while (temp) {
            if (temp->name == name)
                return temp;
            temp = temp->next;
        }
        return nullptr;
    }
};

class Order {
public:
    int orderId;
    string customerName;
    int foodId;
    Order* next;

    Order(int oid, string cname, int fid) {
        orderId = oid;
        customerName = cname;
        foodId = fid;
        next = nullptr;
    }
};

class OrderQueue {
private:
    Order* front;
    Order* rear;
    int count;

public:
    OrderQueue() {
        front = rear = nullptr;
        count = 0;
    }

    void placeOrder(string customerName, int foodId) {
        Order* newOrder = new Order(++count, customerName, foodId);
        if (!rear) {
            front = rear = newOrder;
        } else {
            rear->next = newOrder;
            rear = newOrder;
        }
        cout << "Order placed successfully! Order ID: " << count << endl;
    }

    void deliverOrder() {
        if (!front) {
            cout << "No orders to deliver." << endl;
            return;
        }
        cout << "Delivered Order ID: " << front->orderId << " (" << front->customerName << ")" << endl;
        Order* toDelete = front;
        front = front->next;
        if (!front)
            rear = nullptr;
        delete toDelete;
    }

    void displayQueue() {
        if (!front) {
            cout << "No orders in queue." << endl;
            return;
        }
        Order* temp = front;
        cout << endl << "--- Delivery Queue ---" << endl;
        while (temp) {
            cout << "Order ID: " << temp->orderId << ", Customer: " << temp->customerName << ", Food ID: " << temp->foodId << endl;
            temp = temp->next;
        }
    }
};

int main() {
    if (!login()) return 0;

    Menu menu;
    OrderQueue queue;
    int choice;
    string name;
    double price;
    int id;

    menu.addItem(1, "Burger", 599);
    menu.addItem(2, "Pizza", 700);
    menu.addItem(3, "Fries", 230);
    menu.addItem(4, "Handi", 800);
    menu.addItem(5, "Karahi", 900);
    menu.addItem(6, "Bar BQ", 500);
    menu.addItem(7, "Burger", 700);
    menu.addItem(8, "Chargha", 850);
    menu.addItem(9, "Daal", 300);
    menu.addItem(10, "Vegetable", 250);
    menu.addItem(11, "Pizza", 1200);
    menu.addItem(12, "Egg", 35);

    do {
        cout << endl << "--- Food Ordering & Delivery System ---" << endl;
        cout << "1. Display Menu" << endl;
        cout << "2. Add Menu Item" << endl;
        cout << "3. Delete Menu Item" << endl;
        cout << "4. Update Menu Item" << endl;
        cout << "5. Search Item" << endl;
        cout << "6. Place Order" << endl;
        cout << "7. Deliver Order" << endl;
        cout << "8. View Pending Delivery" << endl;
        cout << "0. Exit" << endl;
        cout << "Enter choice: ";
        cin >> choice;
        cin.ignore();

        switch (choice) {
        case 1:
            menu.displayMenu();
            break;
        case 2:
            cout << "Enter ID: "; cin >> id;
            cin.ignore();
            cout << "Enter Name: "; getline(cin, name);
            cout << "Enter Price: "; cin >> price;
            menu.addItem(id, name, price);
            break;
        case 3:
            cout << "Enter ID to delete: "; cin >> id;
            menu.deleteItem(id);
            break;
        case 4:
            cout << "Enter ID to update: "; cin >> id;
            cin.ignore();
            cout << "New Name: "; getline(cin, name);
            cout << "New Price: "; cin >> price;
            menu.updateItem(id, name, price);
            break;
        case 5:
            cout << "Enter item name to search: ";
            getline(cin, name);
            {
                FoodItem* found = menu.searchLinear(name);
                if (found) {
                    cout << endl << "Item Found:" << endl;
                    cout << "ID: " << found->id << endl;
                    cout << "Name: " << found->name << endl;
                    cout << "Price: $" << fixed << setprecision(2) << found->price << endl;
                } else {
                    cout << "Item not found." << endl;
                }
            }
            break;
        case 6:
            cout << "Enter your name: "; getline(cin, name);
            cout << "Enter Food ID to order: "; cin >> id;
            queue.placeOrder(name, id);
            break;
        case 7:
            queue.deliverOrder();
            break;
        case 8:
            queue.displayQueue();
            break;
        case 0:
            cout << "Exiting..." << endl;
            break;
        default:
            cout << "Invalid option!" << endl;
        }
    } while (choice != 0);

    return 0;
}
