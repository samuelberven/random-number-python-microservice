# Random Number Generator Microservice

A simple microservice built with **ZeroMQ** to communicate between a client and server. The client sends a request (in the form of a stringified integer) to the server, which responds with a JSON array containing a specified number of random integers.

## Features

- **ZeroMQ Communication**: The server and client communicate over ZeroMQ using socket-based messaging.
- **Random Number Generation**: The server generates a list of random integers based on the client’s request.
- **Customizable Parameters**: Clients can specify the number of random numbers, as well as optional upper and lower bounds for the values.

## Installation

To get started with the project, follow these installation steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/bob-microservice.git
    ```

2. Navigate into the project directory:
   ```bash
    cd bob-microservice
    ```

3. Install dependencies:
   ```bash
    pip install pyzmq
   ```

## How It Works
The client sends a request containing the following information:

Number of random numbers to generate.
Lower limit (optional, default is 1).
Upper limit (optional, default is 100).
The server listens for the request, generates the specified number of random integers within the given limits, and returns them as a JSON array.

### Example Request and Response
1. Client Request:
The **client** sends a JSON object with the following array:
   ```python
    request_details = [num_vals, lower_limit, upper_limit + 1]
    request_data = json.dumps(request_details)
    socket.send_string(request_data)
    ```
2. Server Response:
The **server** generates the specified number of random integers and sends them back in a JSON object:
   ```json
    Copy code
    {
      "random_numbers": [26, 44, 74, 49]
    }
   ```

### Request Details:
    ```num_vals```: The number of random numbers to generate.
    ```lower_limit```: The lower bound for the random numbers (default: 1).
    ```upper_limit```: The upper bound for the random numbers (default: 100).

### Example Flow:
1. **Client** (```client.py```) sends a request:
   ```python
   request_details = [10, 1, 100]
   request_data = json.dumps(request_details)
   socket.send_string(request_data)
   ```

2. **Server** (```server.py```) processes the request and generates 10 random numbers between 1 and 100:
    ```json
    {
      "random_numbers": [26, 44, 74, 49, 92, 51, 33, 81, 68, 29]
    }
    ```

## How to Run
### 1. Start the server: To start the server, run the following command:
    ```bash
    python server.py
    ```
### Run the client: After the server is running, you can start the client to send requests. Example:
    ```bash
    python client.py
    ```
### Request format: The client sends a JSON object containing:
- Number of random numbers to generate.
- Lower limit (optional).
- Upper limit (optional).
The server responds with a JSON object containing the array of random numbers.

### Dependencies
**pyzmq**: This library is used for communication between the server and client using ZeroMQ.
Install it via pip:
    ```bash
    pip install pyzmq
    ```

## License
This project is licensed under the MIT License

## References
- [ZeroMQ Documentation](https://zeromq.org/documentation/) - Official documentation for ZeroMQ.
- [Python `pyzmq` Library](https://pyzmq.readthedocs.io/en/latest/) - Python bindings for ZeroMQ.
- [JSON Documentation](https://www.json.org/json-en.html) - Official JSON format documentation.