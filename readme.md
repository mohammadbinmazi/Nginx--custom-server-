**Nginx Server with Node.js**

**Overview**

This project demonstrates the integration of Nginx with Node.js to host three web pages:

Login Page

About Page

Contact Page

Nginx acts as a reverse proxy for the Node.js server, which serves the static HTML pages. The server runs on port 3000 while Nginx listens on the default HTTP port 80.

**Features**

Reverse proxy setup using Nginx.

Node.js serves static HTML files for the Login, About, and Contact pages.

Proper error handling for invalid routes.

Prerequisites

Node.js (version 14.x or higher recommended)

Nginx

**Setup Instructions**

1. Node.js Setup

Clone the repository or download the project files.

Ensure that the following files are in the project directory:

**server.js (main server script)**

login.html

about.html

contact.html

Open a terminal in the project directory and start the Node.js server:

node server.js

Verify the Node.js server is running on http://localhost:3000.

2. Nginx Configuration

Open the Nginx configuration file for editing:

sudo nano /etc/nginx/sites-available/default

**Add the following configuration:**

server {
listen 80;
server_name localhost;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

}

Save the file and exit the editor.

Test the Nginx configuration:

sudo nginx -t

Restart Nginx to apply the changes:

sudo systemctl restart nginx

3. Access the Website

Open a browser and navigate to:

http://localhost/ for the Login page.

http://localhost/about for the About page.

http://localhost/contact for the Contact page.

**File Structure**

project-directory/
|-- server.js
|-- login.html
|-- about.html
|-- contact.html
|-- README.md

**server.js**

The server.js file contains the logic for serving the three web pages based on the requested URL. If an invalid route is requested, a 404 error is returned.
