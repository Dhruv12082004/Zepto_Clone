🛒 Zepto-Inspired Inventory & Order Management System

C++ | Low-Level Design | Design Patterns

A console-based simulation of a Zepto-style grocery delivery platform, implementing dark store selection, inventory management, cart handling, and order fulfillment using strong Low-Level Design (LLD) principles and multiple Design Patterns.

This system models how quick-commerce platforms manage distributed inventory across nearby dark stores and split orders intelligently.

🚀 Features

✅ Multiple Dark Stores with coordinates

✅ Nearby store discovery (distance-based)

✅ Inventory management per store

✅ Cart system

✅ Intelligent order splitting across stores

✅ Multiple delivery partner assignment

✅ Replenishment strategies

✅ Factory-based product creation

✅ Singleton-based system managers

🧠 Design Patterns Used
1️⃣ Factory Pattern

Used in ProductFactory

Product* createProduct(int sku);

Creates product objects dynamically

Decouples product creation logic

Simulates DB-backed product generation

2️⃣ Strategy Pattern

Used for Inventory Replenishment

class ReplenishStrategy

Concrete Strategies:

ThresholdReplenishStrategy

WeeklyReplenishStrategy

Allows dynamic switching of replenishment logic per dark store.

3️⃣ Singleton Pattern

Used in:

DarkStoreManager

OrderManager

Ensures:

Single global access point

Centralized store and order tracking

Controlled object lifecycle

🏗️ System Architecture
User
  ↓
Cart
  ↓
OrderManager (Singleton)
  ↓
DarkStoreManager (Singleton)
  ↓
Nearby DarkStores
  ↓
InventoryManager
  ↓
InventoryStore (DbInventoryStore)
  ↓
Stock Maps
📍 Core Components
🏬 DarkStore

Represents a warehouse/dark store with:

Coordinates (x, y)

Inventory

Replenishment strategy

Supports:

Distance calculation

Stock check

Stock removal

Replenishment

📦 InventoryStore (Abstraction)
class InventoryStore

Concrete Implementation:

DbInventoryStore

Stores:

map<int,int> → SKU to Quantity

map<int,Product*> → SKU to Product

🛍️ Cart

Stores:

vector<pair<Product*, int>>

Handles:

Add item

Calculate total

📑 OrderManager

Responsible for:

Finding nearby dark stores (within 5 KM)

Checking stock availability

Splitting order across stores

Assigning delivery partners

Generating order summary

🔄 Order Fulfillment Logic
Step 1: Find Nearby Stores (≤ 5 KM)

Stores are sorted by distance.

Step 2: Try Single Store Fulfillment

If closest store has all items →
✔ One delivery partner assigned

Step 3: Split Order Across Stores

If not available in one store:

Iterate through nearby stores

Take available quantity

Reduce stock

Assign separate delivery partner per store

Step 4: Compute Total & Print Summary
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
  Splits order across stores
  Assigns multiple delivery partners
  Generates order summary
🧮 Distance Formula Used
sqrt((x - ux)^2 + (y - uy)^2)

Used to determine nearest dark stores.

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

Add payment integration module

Add order status tracking

Add delivery partner tracking system

Introduce database persistence

Add concurrency handling

Add unit tests

📚 Learning Outcomes

This project demonstrates:

Real-world quick-commerce architecture modeling

Multi-store inventory distribution logic

Order splitting optimization

Implementation of multiple design patterns

Scalable system structuring in C++
