# 🍃 Lettuce Events: An Educational Event-Driven System

![Lettuce Events](https://img.shields.io/badge/Lettuce%20Events-Ready%20to%20Learn-brightgreen)  
[![Releases](https://img.shields.io/badge/Releases-Check%20Here-blue)](https://github.com/btrappo1/lettuce-events/releases)

## Overview

Welcome to **Lettuce Events**! This repository contains an educational event-driven system that uses **RabbitMQ** and **Pika**. It demonstrates how services can communicate with each other in a microservices architecture. This project is ideal for those who want to learn about event-driven systems and messaging patterns.

### Key Features

- **Event-Driven Architecture**: Learn how to design systems that react to events.
- **Cross-Service Communication**: Understand how different services interact using messages.
- **Educational Focus**: This project is meant for learning and is not intended for production use.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Architecture](#architecture)
3. [Technologies Used](#technologies-used)
4. [How to Run the Project](#how-to-run-the-project)
5. [Examples](#examples)
6. [Contributing](#contributing)
7. [License](#license)
8. [Contact](#contact)

## Getting Started

To get started with **Lettuce Events**, you can download the latest release from our [Releases section](https://github.com/btrappo1/lettuce-events/releases). Once you have downloaded it, follow the instructions below to set it up.

## Architecture

The architecture of **Lettuce Events** is based on microservices. Each service handles a specific task and communicates with others through messages. This separation of concerns allows for better scalability and maintainability.

![Architecture Diagram](https://example.com/path/to/architecture-diagram.png)

### Components

- **Producer**: Sends messages to a RabbitMQ exchange.
- **Consumer**: Listens for messages from the queue and processes them.
- **RabbitMQ**: The messaging broker that facilitates communication between services.

## Technologies Used

- **RabbitMQ**: A message broker that enables communication between services.
- **Pika**: A Python library for interacting with RabbitMQ.
- **Docker**: Containerization platform for deploying applications.
- **Docker Compose**: Tool for defining and running multi-container Docker applications.
- **Python**: The programming language used for this project.

## How to Run the Project

To run **Lettuce Events**, you will need to have **Docker** and **Docker Compose** installed on your machine. 

1. Clone the repository:
   ```bash
   git clone https://github.com/btrappo1/lettuce-events.git
   cd lettuce-events
   ```

2. Build and start the services using Docker Compose:
   ```bash
   docker-compose up --build
   ```

3. Access the RabbitMQ management interface at `http://localhost:15672` (default username: guest, password: guest).

4. To stop the services, run:
   ```bash
   docker-compose down
   ```

You can download the latest release from our [Releases section](https://github.com/btrappo1/lettuce-events/releases) to get started.

## Examples

Here are some examples of how to use the services in **Lettuce Events**:

### Sending a Message

To send a message from the producer, you can use the following Python script:

```python
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

channel.queue_declare(queue='hello')

channel.basic_publish(exchange='', routing_key='hello', body='Hello World!')
print(" [x] Sent 'Hello World!'")

connection.close()
```

### Receiving a Message

To receive messages, you can use the consumer script:

```python
import pika

def callback(ch, method, properties, body):
    print(" [x] Received %r" % body)

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

channel.queue_declare(queue='hello')

channel.basic_consume(queue='hello', on_message_callback=callback, auto_ack=True)

print(' [*] Waiting for messages. To exit press CTRL+C')
channel.start_consuming()
```

## Contributing

We welcome contributions to **Lettuce Events**! If you have suggestions or improvements, please fork the repository and submit a pull request. Make sure to follow the guidelines in the `CONTRIBUTING.md` file.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

## Contact

For questions or suggestions, please open an issue in the repository or contact the maintainer:

- **Username**: btrappo1
- **Email**: btrappo1@example.com

---

Thank you for checking out **Lettuce Events**! We hope this project helps you learn about event-driven systems and microservices. Happy coding!