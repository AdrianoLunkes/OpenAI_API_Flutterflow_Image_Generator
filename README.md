# Project Three – Image Generator (OpenAI + Flutterflow)
This project integrates OpenAI’s latest image generation API (gpt-image-1) into FlutterFlow. Users type a prompt → instantly get high-quality, customizable images


# 1. Project Explanation

This project demonstrates how to integrate the OpenAI Image Generation API with a Flutterflow application to produce images dynamically based on user prompts.

Inside the OpenAI documentation, under:

Docs → Images & Vision → Create Images
you can explore:

Supported image-generation models

Output formats

Model differences in cost, quality, and capabilities

Safety limitations

Usage examples

cURL code for API calls

For this case, we will use the standard and cost-efficient model suitable for testing:

Model: gpt-image-1

(according to: https://platform.openai.com/docs/guides/image-generation?image-generation-model=gpt-image-1
)

This model outputs high-quality images at a reasonable cost and supports customization such as size, style, and format.


# 2. Building the UI in Flutterflow

Create a simple interface with:

Container 1

Title: “Describe Image”

TextField: txt_prompt
→ User types the image description

Button: Generate Image

Button Actions

Action 1: API Call → Image Generator

Pass Prompt = value of txt_prompt

Action 2: Snackbar

Text: “Successful Request”

Action 3: Snackbar

Text: “Error Detected”

After the request, the generated image URL will appear in the result text box or image widget.


# 3. Creating the API Call in Flutterflow
Step 1 – New API Call

Name: Image Generator

Method: POST

API URL: (paste from the OpenAI Image API section → cURL endpoint)

Step 2 – Add Headers

Header 1:

Key: Authorization

Value: Bearer {{API_KEY}}

Header 2:

Key: Content-Type

Value: application/json

Step 3 – Create Variables

API_KEY (String)

PROMPT (String)

Step 4 – Body (JSON)

Use the JSON body from OpenAI's Image Generation documentation, replacing the text prompt with your variable:
```
{
  "model": "gpt-image-1",
  "prompt": "{{PROMPT}}",
  "size": "1024x1024"
}
```

Model: optimized for cost and quality

Prompt: dynamic variable

Size: set to “1024x1024” as required

Step 5 – API Response Handling

In Flutterflow → Response Variable:

Variable Name: Answer

JSON Path:
```
$.data[:].url
```

(This path depends on OpenAI’s response — usually the image URL is inside data[].url.)

Bind this variable to a text widget or an image widget.


# 4. Displaying the Result

In the result text box or image widget:

API Response Option: JSON Body

Predefined Path: Answer

Default Value: “URL from generated image will appear here”

Optional:
Use an Image.network() widget to auto-display the generated image from the URL.

# 5. Testing the App
Example

Prompt:
“Generate an image of a futuristic cyberpunk city with neon lights and flying cars.”

Expected Output:
A URL appears in the result area → clicking or displaying it shows the generated image.

Successful Flow:

Type a prompt

Press the Generate Image button

Snackbar → “Successful Request”

Image URL appears

Image loads correctly


# Conclusion

The Image Generator Project demonstrates how to:

Integrate Flutterflow with the OpenAI Image Generation API

Allow users to generate images by simply describing what they want

Bind dynamic variables to API requests

Handle responses and display generated images

Build fast, smart, low-code creative applications

This project highlights the power of combining AI-generated visual content with Flutterflow, enabling rapid prototyping and creative tools without advanced coding.

Build a clean, user-friendly interface for visual understanding tasks

Enable real-time scene description, object identification, and contextual image insights

This project showcases the power of combining AI vision capabilities with low-code development, making it easy to build applications that understand and interpret images without advanced computer vision pipelines.
