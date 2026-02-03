
📊 AI-Powered PPTGenerator
A Python tool that automatically generates professional PowerPoint presentations using Google Gemini for content creation and Pexels for relevant imagery.

🚀 Features
Automated Content Creation: Uses gemini-2.5-pro to generate structured slide outlines, bullet points, and titles based on a simple topic prompt.

Smart Image Sourcing: Analyzes slide content to generate relevant search queries, fetching high-quality images via the Pexels API.

Dynamic Layouts: Automatically selects between Title, Content, and Image-heavy slide layouts.

Robust Fallbacks: Includes fallback mechanisms for content generation failure or missing images to ensure a presentation is always produced.

🛠️ Prerequisites
Before running the script, ensure you have the following:

Python 3.8+

Google Gemini API Key (Get it here)

Pexels API Key (Get it here)

📦 Installation
Clone the repository (or save the script):

Bash
git clone https://github.com/yourusername/ppt-generator.git
cd ppt-generator
Install required dependencies: You will need google-generativeai, python-pptx, requests, and Pillow.

Bash
pip install google-generativeai python-pptx requests Pillow
⚙️ Configuration
1. Set up the Pexels API Key
Important: The provided code has an empty placeholder for the Pexels API key. You must modify the download_image method in the script or add an environment variable.

Option A (Recommended): Modify code to use Env Variable Change line 102 in your script to:

Python
'Authorization': os.getenv('PEXELS_API_KEY')
Option B: Hardcode (Not recommended for sharing) Paste your key directly into the headers dictionary:

Python
'Authorization': 'YOUR_PEXELS_API_KEY_HERE'
2. Set Environment Variables
Set your API keys in your terminal or .env file:

Linux/Mac:

Bash
export GEMINI_API_KEY="your_gemini_key_here"
export PEXELS_API_KEY="your_pexels_key_here"
Windows (PowerShell):

PowerShell
$env:GEMINI_API_KEY="your_gemini_key_here"
$env:PEXELS_API_KEY="your_pexels_key_here"
💻 Usage
Here is a simple example of how to use the PPTGenerator class in your main script:

Python
from ppt_generator import PPTGenerator # Assuming you saved the class in ppt_generator.py
import os

# Ensure API keys are set, or pass them directly
api_key = os.getenv("GEMINI_API_KEY")

# Initialize the generator
generator = PPTGenerator(api_key=api_key)

# Generate a presentation
# Arguments: Topic, Number of Slides, Output Filename
generator.generate_presentation(
    topic=" The Future of Quantum Computing",
    num_slides=7,
    output_path="Quantum_Future.pptx"
)
🧩 Class Overview
PPTGenerator
__init__(api_key): Initializes the Gemini model and the empty presentation object.

generate_content_outline(topic, num_slides): Prompts Gemini to create a JSON-structured outline of the presentation.

generate_image_description(slide_content): Converts slide text into a short, searchable keyword string for image sourcing.

download_image(query): Fetches an image from Pexels and saves it locally temporarily.

generate_presentation(topic, ...): The main driver function that orchestrates the outline creation, slide generation, and saving process.

⚠️ Troubleshooting
JSON Parsing Error: If Gemini returns unstructured text, the script uses a hardcoded _get_fallback_outline method to ensure a PPT is still generated.

Image Download Failures: If Pexels fails or no image is found, a solid color placeholder image is generated using Pillow.

401 Unauthorized: Ensure your Pexels API Key is correctly pasted in the headers dictionary inside the download_image method.
