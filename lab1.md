## Lab1 (pate1595):

### Youtube video link: 
-  https://youtu.be/qPaUq4XMzQQ

## <b> Explaination:- </b><br>

### Store Front (Vue.js):

The Store Front web application allows customers to browse products, examine details, and place orders. It is built with Vue.js, which includes reactive UI components and client-side state management for an effortless shopping experience, such as search, product filters, cart, and checkout.

It communicates with the back end via HTTP, calling the Product Service to retrieve product listings and details (GET /products) and sending orders to the Order Service (POST /orders). The Store Front, which is commonly hosted on port 8080, handles input validation and customer feedback (order confirmations and error notifications).

### Order Service (Node.js):

The Order Service is responsible for accepting and processing orders from the Store Front. It is built with Node.js, validates incoming order requests, generates an order record or acknowledgement for the front end, and controls the order lifecycle (accept, reject, confirm).

To ensure reliable, decoupled processing it uses RabbitMQ as a message broker: after accepting an order, the service publishes an order message to a queue so downstream components can process it asynchronously. The Order Service also exposes REST endpoints used by the front end and runs on an API port 3000.

### Product Service (Rust):

The Product Service manages product data names, descriptions, prices, and inventory levels, and exposes APIs for consumers to read or update that data. It is written in Rust for performance and memory-safety, making it suitable for a service responsible for consistent product lookups and stock operations.

The Store Front queries this service to display product listings (GET /products, GET /products/:id). Inventory can be checked synchronously by the Order Service during order validation, or the Product Service can be updated asynchronously (depending on implementation) when order messages are processed. The Product Service typically listens on a service port such as 3030.

## Conclusion

In a simple way the flow is:
- Customer uses the Store Front  
- Store Front calls Product Service for product data  
- Store Front calls Order Service to place orders  
- Order Service passes orders into RabbitMQ  
- RabbitMQ ensures reliable order delivery to processing systems


