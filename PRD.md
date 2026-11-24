**Project Requirements Document (PRD)**
**COS209 Backend Engineering**
**Team: Group 10**
**Date: [2026-11-22]**

**1. Executive Summary**
**Objective**
The aim of this project is to create a delivery service system that will make it easy for people to send and receive goods. Customers will be able to place delivery orders, check the status of their deliveries, and know when their items will arrive. The system will also help manage delivery riders and orders.

**Target Users**
Customers who want to send or receive items.
Delivery riders who deliver items.
Admins who manage the delivery service.
Shop owners who need people to deliver their goods.

**2. Problem Statement & User Research**
**The Core Problem**
Many students do not know what supplies or food are currently available in campus stores. This can make a trip unsuccessful and waste time and energy. Students who are studying or resting in their hostels may also need snacks, drinks, or other supplies. Going out from distant hostels can be tiring and time-consuming. Ordering from businesses that use WhatsApp can cause delays when the salesperson is unavailable or does not know what is in stock. This problem is especially noticeable during exam periods and weekends. At these times, students would rather stay in their halls to study and do not know what is available in nearby stores or shops.

**Current Workarounds & Limitations**
**How People Cope Today**
When students with busy schedules run out of supplies such as painkillers, sanitary pads, stationery, or snacks, they may knock on neighboring room doors or post in hall or hostel group chats to borrow items. This method may work or fail, depending on what their neighbors have. It does not reliably meet urgent needs and may create awkward obligations when borrowed items are replaced later.
**Communicating with Vendors via Texting**
Regular customers collect vendors' contact information and ask whether food or a particular item is available before going to the store. This method does not work well during rush hours, because vendors may be busy serving physical queues and cannot answer calls or WhatsApp messages. It relies on personal familiarity rather than a public platform and does not provide delivery after availability is confirmed.
**Why Existing Methods Fail**
**Zero Visibility Before Effort:** A student or another person may make the trip before the stock is confirmed. If the item is unavailable, the time, transportation, and effort will have been wasted.
**The Lack of Accountability and Standardization**
Informal delivery arrangements and hostel borrowing have no clear way to resolve problems if an item arrives in the wrong condition, is cold, or is late.
**Interview & Survey Findings**
**Finding 1**
Michael is a 300-level IT student who must balance student responsibilities with academic work. He has little time for shopping and socializing.
**Finding 2**
Professor Oni is a lecturer in the Medicine department and lives alone at Babcock during the weekdays, returning home to Lagos on weekends. With his surgeries and classes, he barely gets a chance to go out and get a bite to eat. During my conversation with him, he said, "I wish the school had a central delivery service to make it easier to get a bite."
**Finding 3**
Martins is a 400-level medical laboratory science student and athlete. He is very busy and barely has time to find healthy food options.

**3. Proposed Solution & MVP Scope**
**High-Level Solution**
The campus delivery service is a simple application that allows students to order food, snacks, and other items from stores on or near campus. Orders are delivered to students at their hostels or lecture halls. Students often waste time walking or waiting in queues, especially during lectures or bad weather, and campus delivery is not well organized. This system connects students with shop owners and delivery riders. Students can check available items, place an order, make a payment, and track the order until it arrives.

**Minimum Viable Product (MVP) Features**
1. Browse and Order: Students see vendors and their items, add what they want to a cart, and place an order with their delivery location. This is a must-have because without it there is nothing to deliver.
2. Rider Assignment and Delivery: The system sends each order to an available rider. The rider accepts the order, picks it up from the shop, and delivers it. This is a must-have because it is the main purpose of the delivery service.
3. Order Tracking and Payment: Students pay for their orders and view their status, such as received, being prepared, on the way, or delivered. This is a must-have because it builds trust and helps make sure that shops and riders are paid.

**Out of Scope (Future Versions)**
- Live map tracking of riders
- Ratings and reviews for vendors and riders
- Scheduled and repeat orders
- Discount codes and loyalty rewards
- Delivery outside the campus area
- A separate admin dashboard with detailed reports

**4. Backend Architecture & Data Requirements**

**Core Data Entities**
User:* id, name, role (customer, rider, shop_owner, admin), phone, hostel_address, created_at
Shop:* id, owner_id, name, location, is_open
Product: id, shop_id, name, price, stock_quantity, updated_at
Order: id, customer_id, shop_id, delivery_address, total_price, status, created_at
OrderItem: id, order_id, product_id, quantity, unit_price
Delivery: id, order_id, rider_id, status, picked_up_at, delivered_at

**Core System Workflows**
1. **Placing an Order:** Customer browses a shop's products -> System checks each item's stock -> System creates the order, reduces stock, and sets status to "pending" -> Shop owner is notified.
2. **Confirming & Assigning:** Shop owner accepts the order -> System assigns an available rider -> Rider is notified, and the customer sees "Rider assigned".
3. **Delivery Tracking:** Rider updates status (picked up -> on the way -> delivered) -> System saves each change with a timestamp -> Customer sees the updated status.
4. **Updating Stock:** Shop owner changes a product's quantity or marks it as out of stock -> System saves the change -> Customers see current availability immediately.

**Non-Functional Requirements**
**Security & Access Control:** Customers can view only their own orders. Riders can see only the orders assigned to them. Shop owners can manage only their own shops and products. Admins can view and manage everything. Users log in with hashed passwords.
**Data Integrity & Validation:** Stock can never go below zero. An order must have at least one item. Phone numbers and addresses are required. A rider cannot be assigned to two active deliveries at once. Duplicate submissions of the same order are rejected.
**Reliability:** If an order fails halfway, the stock reduction is rolled back. Order status updates are saved even if the user's connection drops. At peak times, such as exam weeks, the system queues orders instead of rejecting them.

**5. Success Metrics**

How we will know if the MVP actually worked:

1. If we can bring the average resolution time down from like 3 days to less than 12 hours. That is our main goal.
2. We want atleast 500 students to use it in the first month and most of them keep coming back weekly.
3. We will do a quick survey after they use it, we are targeting like 4 star rating and positive feedbacks.
4. Also for the admins, it should reduce there manual work. Like cutting the time they spend by half.

GROUP MEMBERS
Fakolade Obanijesu Samuel 
25/0211(5)
Akinbayo Oluwafeyikemi David
25/0929(1)
Babalola folajimi David 
25/1872(3,4)
FADARE NOEL OLUWAFUNTO
25/0438(2)