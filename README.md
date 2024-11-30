These are the servers this weather application are being hosted on 
Web01   54.173.1.14
web02 52.55.180.37
lb 54.197.195.250
I apologise for the multiple submissioons please bear with me 


## Overview
This is a weather application that allows users to search for current weather and hourly forecasts of cities around the world. It fetches data from the OpenWeatherMap API and displays the information in a user-friendly format.

The application is deployed across two web servers (`Web01` and `Web02`) with a load balancer to ensure scalability and high availability.

## Features
- Search for weather by city.
- View current weather conditions (temperature, description, and weather icon).
- View hourly weather forecast for the next 24 hours (3-hour intervals).
- Responsive and user-friendly interface.

## External API
The app utilizes the **OpenWeatherMap API** to fetch weather data. You will need an API key to access the service. For development, the API key used is `b25b4d0fdd8f898731db46ef4ddc299b`. Replace it with your own API key for production.

API Documentation: [OpenWeatherMap API](https://openweathermap.org/api)

## Setup Instructions

### Part 1: Local Setup
1. Clone the repository to your local machine.
 
Navigate to the project directory.

bash
Copy code
cd weather-app
Open index.html in your browser to view the app locally.

Part 2: Server Setup
This app has been deployed on two web servers and a load balancer.

Web Server 1 (Web01):
IP Address: 54.173.1.14
Operating System: Ubuntu 20.04
Nginx is configured to serve the weather app.
Web Server 2 (Web02):
IP Address: 52.55.180.37
Operating System: Ubuntu 20.04
Nginx is configured to serve the weather app.
Load Balancer (Lb01):
IP Address: 54.197.195.250
HAProxy is configured to load balance traffic between Web01 and Web02.
Nginx Configuration (Web Servers)
Nginx is used as the web server on both Web01 and Web02. Below is the basic Nginx configuration file for serving the app:

nginx
Copy code
server {
    listen 80;
    server_name localhost;

    
}
Load Balancer (HAProxy)
The load balancer (Lb01) is configured to distribute incoming requests between the two web servers.

HAProxy Configuration:
haproxy
Copy code
frontend http_front
   bind *:80
   default_backend http_back

backend http_back
   balance roundrobin
   server web-01 54.173.1.14:80 check
   server web-02 52.55.180.37:80 check
Deployment Instructions
Clone the app repository on both Web01 and Web02.

bash
Copy code
git clone https://github.com/yourusername/weather-app.git
Install Nginx on both web servers:

bash
Copy code
sudo apt update
sudo apt install nginx
Configure Nginx to serve the weather app by editing the Nginx configuration file.

Restart Nginx:

bash
Copy code
sudo systemctl restart nginx
On Lb01, configure HAProxy to load balance between Web01 and Web02.

Restart HAProxy:

bash
Copy code
sudo systemctl restart haproxy
Testing the Application
Once everything is set up, navigate to the load balancer's IP address (54.197.195.250) in a web browser. You should see the weather app.
Refresh the page multiple times to ensure that the traffic is being properly balanced between Web01 and Web02.
Troubleshooting
404 Error: Ensure that the app files are correctly placed in the specified directory (/home/ubuntu/Weather-app) on both web servers.
API Errors: If there are issues with fetching weather data, ensure that your API key is correct and check the OpenWeatherMap API documentation for any potential rate limits or issues.
Contributions
If you wish to contribute to this project, feel free to fork the repository and submit a pull request.

License
This project is licensed under the MIT License.




