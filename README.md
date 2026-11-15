
# NationDev AI Coding Assistant

## 1. Project Overview

This project is a web-based AI Coding Assistant developed for the NationDev Generative AI assignment.

The application helps users understand programming concepts, generate code examples, debug errors, and ask follow-up coding questions.

It uses Google Gemini to generate responses through a Python Flask application hosted on Amazon Web Services (AWS).

**Live application:** http://13.60.71.74/

**GitHub repository:** https://github.com/MusdafOmar/nation-ai-chatbot

Note: The repository is private, so access must be granted to anyone who needs to review the source code.

## 2. Research and Planning

### Project Idea

I chose to build an AI Coding Assistant because programming students often need help understanding code, fixing errors, and learning new concepts.

My goal was to develop a simple web application where users could ask programming questions and receive clear explanations.

### Technologies Selected

- Python: Application programming language.
- Flask: Lightweight Python web framework.
- Google Gemini API: Generates AI-powered coding responses.
- HTML, CSS, and JavaScript: Web interface.
- Marked.js: Displays Markdown-formatted answers.
- DOMPurify: Sanitizes rendered HTML.
- Git and GitHub: Source code version control.
- AWS EC2: Cloud hosting.
- Gunicorn: Python application server.
- Nginx: Reverse proxy web server.
- systemd: Manages the application as a background service.

### Architecture

User Browser
    |
    v
AWS EC2 Public IP (HTTP Port 80)
    |
    v
Nginx Reverse Proxy
    |
    v
Gunicorn (127.0.0.1:8000)
    |
    v
Flask Application
    |
    v
Google Gemini API

The application sends the user's question to Gemini and displays the generated response in the browser.

## 3. Implementation

### Phase 1: Local Development

I created a Python project and configured a virtual environment.

I installed Flask, the Google GenAI SDK, python-dotenv, and other required dependencies.

I developed a Flask application with two main routes:

- `/`: Displays the chatbot interface.
- `/chat`: Receives questions and returns AI-generated responses.

I used HTML, CSS, and JavaScript to create a responsive chat interface.

The interface supports Markdown responses, code blocks, conversation history, and a loading indicator.

### Phase 2: Gemini Integration

I connected the application to Google's Gemini API.

The application reads the API key from an environment file instead of placing it directly in the source code.

I configured the chatbot to provide beginner-friendly programming explanations, debugging help, and code examples.

The application also uses recent conversation history to understand follow-up questions.

### Phase 3: GitHub

I created a GitHub repository to manage the project source code.

I configured `.gitignore` to exclude sensitive and environment-specific files, including `.env` and `.venv`.

The repository was kept private during development.

### Phase 4: AWS Deployment

I launched an Ubuntu EC2 instance in the AWS Europe (Stockholm) region.

I configured the instance's security group to allow SSH access from my IP address and public HTTP access.

I cloned the project from GitHub using a read-only deploy key.

I installed the Python dependencies inside a virtual environment on the server.

I securely transferred the environment configuration to the EC2 instance.

I tested the Gemini API connection from AWS before starting the web application.

### Phase 5: Production Application Server

I installed Gunicorn and configured it to run the Flask application on `127.0.0.1:8000`.

I created a systemd service to start the application automatically and restart it if the process fails.

I installed Nginx and configured it as a reverse proxy.

Nginx accepts HTTP requests on port 80 and forwards them to Gunicorn.

The chatbot became accessible through the EC2 public IP address.

## 4. Security Measures

I implemented several basic security measures:

- Stored the Gemini API key in a `.env` file.
- Excluded `.env` from Git.
- Restricted the server environment file permissions.
- Used SSH key authentication.
- Restricted SSH access using the AWS security group.
- Kept Gunicorn bound to the local interface.
- Used Nginx as the public reverse proxy.
- Limited question length to 4,000 characters.
- Validated conversation history and accepted roles.
- Limited conversation history to the latest 10 entries.
- Disabled Flask debug mode.
- Added Nginx rate limiting to the `/chat` endpoint.

The Nginx rate limit is configured for 10 requests per minute per IP address, with a small burst allowance.

The application currently uses HTTP rather than HTTPS. HTTPS, authentication, and stronger API usage controls are possible future improvements.

## 5. Testing and Results

### Local Testing

I tested the Flask application locally and confirmed that Gemini generated programming answers.

I also tested follow-up conversation functionality.

### AWS Application Testing

I verified that the Gemini API worked directly from the EC2 server.

I confirmed that Gunicorn successfully served the Flask application.

The internal HTTP test returned:

HTTP 200 OK

### Public Website Testing

I accessed the application using its public AWS IP address.

The public homepage returned:

HTTP 200 OK

I submitted a programming question asking the chatbot to explain how to check whether a number is even or odd.

The chatbot generated a correct Python function and explained the modulo operator.

I also tested a question about calculating the square of a number.

The chatbot returned a correct Python function using the exponentiation operator.

### Rate-Limit Testing

I tested the `/chat` endpoint with eight consecutive invalid requests.

Results:

- Requests 1–4: HTTP 400 (invalid input).
- Requests 5–8: HTTP 429 (rate limit applied).

This confirmed that Nginx rejected excessive requests before they reached the Gemini API.

## 6. Problems Encountered and Solutions

### Problem 1: SSH Connection Timeout

I experienced an SSH connection timeout when connecting to AWS.

The security group was configured for an earlier public IP address.

**Solution:** I updated the SSH security group rule to allow my current public IP address.

### Problem 2: Gemini API Authentication

The application initially experienced a Gemini API authentication problem on AWS.

**Solution:** I verified the environment configuration, securely transferred the correct credentials, and successfully tested the Gemini connection from EC2.

### Problem 3: Gunicorn Process Stopped

Gunicorn initially started in an interactive SSH session but was no longer running when I tested it later.

**Solution:** I created a systemd service to manage Gunicorn independently of the SSH session.

### Problem 4: Public Web Access

Gunicorn was accessible internally but was not intended to be exposed directly to the internet.

**Solution:** I configured Nginx to accept public HTTP traffic and forward requests to Gunicorn on the local interface.

### Problem 5: Excessive API Requests

A publicly accessible chatbot can receive repeated requests that consume AI API quota.

**Solution:** I configured Nginx request rate limiting and verified that excessive requests returned HTTP 429.

## 7. Conclusion

I successfully developed and deployed an AI Coding Assistant using Flask, Google Gemini, and AWS EC2.

The application can answer programming questions, generate code examples, explain programming concepts, and support follow-up questions.

Through this project, I learned how to integrate a generative AI API, develop a web application, manage code with GitHub, configure an AWS server, deploy an application with Gunicorn and Nginx, and implement basic security controls.

The most valuable learning experience was troubleshooting real deployment problems and verifying each component step by step.

## 8. Future Improvements

Possible improvements include:

- Configure HTTPS using a domain and TLS certificate.
- Add user authentication.
- Implement stronger API quota and cost controls.
- Add automated tests and continuous integration.
- Improve the interface and accessibility.
- Add application monitoring and logging.
- Add support for saving conversations.

## 9. Author

Developed for the NationDev Generative AI assignment.
