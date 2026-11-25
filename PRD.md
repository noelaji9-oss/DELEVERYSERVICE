**Project Requirements Document (PRD)**
**COS209 Backend Engineering**
**Team: Group 10**
**Date: [2026-11-22]**

**1. Executive Summary**
**Product Overview**
This service helps people on campus order food and other items from nearby shops. Customers can see what is available, place an order, pay, and have a rider deliver it.

**Objective**
The goal is to make it easier for people to send and receive items. Customers can place orders and follow their progress. The system also helps shops and riders manage deliveries.

**Business Objectives**
- Make food and everyday items easier to get on campus.
- Help customers spend less time looking for and collecting items.
- Make deliveries more dependable and easier to track.
- Encourage students to use the service regularly and reduce the work administrators do by hand.

**Target Users**
- Customers who want to order or send items.
- Riders who deliver orders.
- Administrators who manage the service.
- Shop owners who sell goods and need them delivered.

**Stakeholders**
- Customers: choose items, place orders, pay, and check delivery progress.
- Shop owners: add products, update stock, and prepare orders.
- Riders: accept deliveries and report their progress.
- Administrators: oversee the service and help manage problems.

**2. Problem Statement & User Research**
**The Core Problem**
Students often do not know which food or supplies nearby shops have in stock. They may walk to a shop only to find that an item is unavailable. Students studying or resting in their hostels may also need snacks, drinks, or other supplies but find it tiring to go out. Asking shops through WhatsApp can take time, especially when staff are busy or do not know the current stock. This is a bigger problem during exams and weekends, when students may prefer to stay in their halls.

**Current Workarounds & Limitations**
**How People Cope Today**
When students run out of items such as painkillers, sanitary pads, stationery, or snacks, they may ask neighbors or post in hostel group chats to borrow them. This only works if someone nearby has the item, so it may not help when the need is urgent. Borrowing can also leave students feeling they must replace the item later.
**Communicating with Vendors via Texting**
Some customers message shops to ask if an item is available before visiting. During busy times, shop staff may not be able to answer calls or messages. Customers also need to know the shop's contact details, and confirming that an item is available does not arrange delivery.
**Why Existing Methods Fail**
**No Clear Stock Information:** People may travel to a shop before finding out whether an item is available. If it is out of stock, the trip is wasted.
**No Clear Way to Handle Problems:** Informal deliveries do not have a consistent way to deal with late orders or items that arrive in poor condition.
**User Stories and Functions**
1. **Browse and Order Items:** As a busy 300-level IT student, I want to see available items and order them for delivery so that I can get what I need without shopping in person.
2. **Order Meals for Delivery:** As a busy lecturer, I want to order meals from campus shops and have them delivered so that I can eat without leaving work or home.
3. **Discover Healthy Food:** As a busy 400-level medical laboratory science student and athlete, I want to find and order healthy food so that I can eat well even when I have little time to shop.

**3. Proposed Solution & MVP Scope**
**High-Level Solution**
The application lets students order food, snacks, and other items from shops on or near campus. A rider delivers orders to places such as hostels or lecture halls. Students can see available items, place an order, pay, and check its progress. The service connects customers, shop owners, and riders.

**Minimum Viable Product (MVP) Features**
An MVP (Minimum Viable Product) is the smallest useful version of a product. All features below are Must Have (needed for launch). No Should Have (important but able to wait) or Could Have (optional) features have been agreed. Items under “Out of Scope” are Won't Have in this release.
1. Browse and Order: Students can look at shops and items, add items to a cart, and order them for delivery.
2. Assign a Rider and Deliver: The system assigns an available rider to an order. The rider accepts the job, picks up the order, and delivers it.
3. Track and Pay for Orders: Students can pay and see whether an order has been received, is being prepared, is on the way, or has been delivered.

**Functional Requirements**
Functional requirements describe actions the system must support.
1. Customers can browse shops and see their products and current stock.
2. Customers can place an order with at least one item and a delivery location.
3. The system checks stock, creates the order, updates stock, and tells the shop owner about the order.
4. Shop owners can accept orders and change product stock. Accepted orders are assigned to an available rider.
5. Riders can update delivery progress, and customers can see the latest order status.
6. Customers can pay for orders. The payment methods and payment rules still need to be decided.

**Acceptance Criteria**
Acceptance criteria are checks that show whether a feature works as expected.
- An order is accepted only if it has at least one available item and a delivery location.
- If an order fails, the system does not reduce the stock. Stock must never go below zero.
- When a shop owner accepts an order, an available rider is assigned and notified.
- The rider can update the delivery status. The customer can see each update and when it happened.
- When the rider marks an order as delivered, the system saves the delivery time.

**Out of Scope (Future Versions)**
- Showing riders moving on a live map.
- Ratings and reviews for shops and riders.
- Orders scheduled for later or repeated regularly.
- Discount codes and loyalty rewards.
- Deliveries outside the campus area.
- A separate admin page with detailed reports.

**Assumptions and Open Questions**
**Assumptions**
- The first release serves customers and shops on or near campus.
- Shop owners keep product stock information up to date.
- Customers provide a delivery location when they order.

**Open Questions**
- How far from campus can riders deliver, and how much will delivery cost?
- Which payment methods will be available, and when will customers pay?
- How can a customer cancel an order, get a refund, or report a delivery problem?

**4. Backend Architecture & Data Requirements**

**Core Data Entities**
These are the main types of information the system needs to store. An ID is a unique value used to tell one record from another. Times show when something happened.
- User: id, name, role (customer, rider, shop_owner, or admin), phone, hostel_address (hostel address), created_at (account creation time).
- Shop: id, owner_id (shop owner's user id), name, location, is_open (whether the shop is open).
- Product: id, shop_id, name, price, stock_quantity (number of items in stock), updated_at (last update time).
- Order: id, customer_id, shop_id, delivery_address, total_price, status, created_at (order time).
- OrderItem: id, order_id, product_id, quantity, unit_price (price per item when ordered).
- Delivery: id, order_id, rider_id, status, picked_up_at (pickup time), delivered_at (delivery time).

**Core System Workflows**
These are the main steps people and the system follow to complete common tasks.
1. **Placing an Order:** The customer chooses products. The system checks that they are in stock, creates the order, reduces the stock, marks the order as “pending,” and tells the shop owner.
2. **Confirming and Assigning:** The shop owner accepts the order. The system assigns an available rider, tells the rider, and shows the customer that a rider has been assigned.
3. **Tracking a Delivery:** The rider marks the order as picked up, on the way, and delivered. The system saves the time of each update and shows the latest status to the customer.
4. **Updating Stock:** The shop owner changes a product's quantity or marks it as out of stock. The system saves the change so customers see the current availability.

**Non-Functional Requirements**
These requirements describe how safely and reliably the system must work.
**Security and Access:** Customers can see only their own orders. Riders can see only deliveries assigned to them. Shop owners can manage only their own shops and products. Admins can manage all records. Passwords must be stored in a protected, hashed form, not as readable text.
**Correct Data:** Stock must never go below zero. Every order must contain at least one item. Phone numbers and delivery addresses are required. A rider cannot have two active deliveries at once. Repeating the same order submission must not create duplicate orders.
**Reliability:** If placing an order fails, the stock change must be undone. Status updates must be saved with their times. When many orders arrive at once, the system should queue them instead of rejecting them.

**5. Success Metrics**

These are the goals we will use to check whether the first version is helping:

1. Resolve order problems in less than 12 hours on average, down from about 3 days.
2. Have at least 500 students use the service in its first month, with many returning each week.
3. Aim for an average user rating of 4 out of 5 stars and positive feedback.
4. Cut the time admins spend on manual work by half.

GROUP MEMBERS
Fakolade Obanijesu Samuel 
25/0211(5)
Akinbayo Oluwafeyikemi David
25/0929(1)
Babalola folajimi David 
25/1872(3,4)
FADARE NOEL OLUWAFUNTO
25/0438(2)