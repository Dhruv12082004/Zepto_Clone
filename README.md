🛒 Zepto Clone – Inventory & Order Management System

C++ | Low-Level Design | Design Patterns

A console-based simulation of a Zepto-style quick commerce platform that manages distributed dark store inventory, cart handling, intelligent order splitting, and delivery partner assignment using strong Low-Level Design principles.

🚀 Features

📍 Multiple Dark Stores with coordinates

📦 Per-store inventory management

🔍 Nearby store discovery (within 5 KM)

🛍️ Cart management

🔄 Intelligent order splitting across stores

🚚 Multiple delivery partner assignment

🏭 Factory-based product creation

🎯 Strategy-based replenishment

🔒 Singleton-based system managers

🧠 Design Patterns Used
1️⃣ Factory Pattern

Used in ProductFactory to create product objects dynamically.

2️⃣ Strategy Pattern

Used for inventory replenishment:

ThresholdReplenishStrategy

WeeklyReplenishStrategy

3️⃣ Singleton Pattern

Used in:

DarkStoreManager

OrderManager

Ensures centralized management and single instance control.

🏗️ System Architecture
User
  ↓
Cart
  ↓
OrderManager (Singleton)
  ↓
DarkStoreManager (Singleton)
  ↓
Nearby DarkStores (≤ 5 KM)
  ↓
InventoryManager
  ↓
InventoryStore (DbInventoryStore)
  ↓
Stock Maps (SKU → Quantity)
📦 Core Components
🏬 DarkStore

Represents a warehouse with:

Name

Coordinates (x, y)

InventoryManager

Replenishment Strategy

Supports:

Distance calculation

Stock checking

Stock removal

Replenishment execution

📦 InventoryStore (Abstraction)

Stores inventory using:

map<int, int> → SKU to Quantity

map<int, Product*> → SKU to Product

Concrete implementation:

DbInventoryStore

🛍️ Cart

Stores:

vector<pair<Product*, int>>

Supports:

Adding items

Calculating total amount

📑 OrderManager

Responsible for:

Finding nearby dark stores

Checking stock availability

Single-store fulfillment

Multi-store order splitting

Assigning delivery partners

Printing order summary

🔄 Order Fulfillment Logic
Step 1 – Find Nearby Stores

Uses Euclidean distance formula:

sqrt((x - ux)*(x - ux) + (y - uy)*(y - uy))

Stores within 5 KM are considered.

Step 2 – Single Store Fulfillment

If the closest store has all required items:

Remove stock

Assign one delivery partner

Complete order

Step 3 – Multi-Store Order Splitting

If one store cannot fulfill the entire order:

Iterate over nearby stores

Allocate available quantities

Assign delivery partner per store

Track unfulfilled items (if any)

📌 Example Flow
User: Aditya (1,1)

Nearby Stores:
  DarkStoreA
  DarkStoreC
  DarkStoreB

Cart:
  Apple x4
  Banana x3
  Chocolate x2

System:
  Splits order across multiple stores
  Assigns multiple delivery partners
  Generates final order summary
💻 How to Run
Compile
g++ zepto.cpp -o zepto
Run
./zepto
🎯 LLD Concepts Demonstrated

Encapsulation

Abstraction

Delegation

Separation of Concerns

Open/Closed Principle

Loose Coupling

Dynamic Strategy Switching

Multi-warehouse inventory allocation

⚡ Possible Improvements

Replace raw pointers with smart pointers

Add persistent database storage

Integrate payment module

Add delivery tracking

Introduce concurrency handling

Add unit tests
