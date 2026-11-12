# NationDev AI Coding Assistant

A web-based AI coding assistant developed as part of the NationDev Generative AI assignment.

## Project Overview

This application helps users learn programming, understand code, debug errors, and ask follow-up coding questions.

It uses Google Gemini to generate AI-powered responses through a Flask web application.

## Features

- AI-powered programming assistance
- Beginner-friendly coding explanations
- Python and other programming examples
- Markdown-formatted responses
- Readable code blocks
- Conversation history for follow-up questions
- Loading indicator while generating responses
- Responsive web interface

## Technologies

- Python
- Flask
- Google Gemini API
- HTML, CSS, and JavaScript
- Marked.js and DOMPurify
- Git and GitHub

## Installation

1. Clone the GitHub repository.
2. Create a Python virtual environment.
3. Activate the virtual environment.
4. Install dependencies:

   pip install -r requirements.txt

5. Create a `.env` file containing:

   GEMINI_API_KEY=your_api_key_here
   GEMINI_MODEL=gemini-3.5-flash-lite

6. Start the application:

   python app.py

7. Open http://127.0.0.1:5000 in your browser.

## Security

API keys are stored in a local `.env` file and excluded from Git using `.gitignore`.

The Flask development server is intended for local testing only.

## Project Status

Local development and initial testing are complete.

AWS deployment, production security improvements, and final assignment documentation are in progress.

## Future Improvements

- Improved interface styling
- More robust error handling
- Additional security and API usage controls
- Automated testing
- Production deployment on AWS

## Author

Developed for the NationDev Generative AI assignment.
