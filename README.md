## Prototype Development for Image Generation Using the Stable Diffusion Model and Gradio Framework

### AIM:
To design and deploy a prototype application for image generation utilizing the Stable Diffusion model, integrated with the Gradio UI framework for interactive user engagement and evaluation.

### PROBLEM STATEMENT:
Develop an accessible and user-friendly platform for generating high-quality images from text prompts using the Stable Diffusion model. The application must allow real-time user interaction, customizable settings for image generation, and facilitate evaluation and feedback from users.

### DESIGN STEPS:

#### STEP 1:Model Setup
Install the required libraries: transformers, diffusers, torch, and gradio.
Load the Stable Diffusion model using the diffusers library.

#### STEP 2:Define Image Generation Function
Create a Python function to take a text prompt as input and generate an image using the model.
Allow optional parameters like image resolution, number of inference steps, and guidance scale for flexibility.


#### STEP 3: Integrate with Gradio UI
Design a Gradio interface to accept user input and display generated images.
Configure sliders or text boxes for user-controlled parameters (e.g., resolution, style).
Deploy the application on a local server or a cloud platform.

### PROGRAM:
```
from diffusers import StableDiffusionPipeline
import torch
import gradio as gr

# Load the Stable Diffusion model
pipe = StableDiffusionPipeline.from_pretrained("runwayml/stable-diffusion-v1-5")
pipe.to("cuda")

# Define the image generation function
def generate_image(prompt, steps, guidance):
    image = pipe(prompt, num_inference_steps=steps, guidance_scale=guidance).images[0]
    return image

# Gradio interface
interface = gr.Interface(
    fn=generate_image,
    inputs=[
        gr.Textbox(label="Enter a prompt", placeholder="e.g., A futuristic cityscape"),
        gr.Slider(label="Steps", minimum=10, maximum=50, step=5, value=20),
        gr.Slider(label="Guidance Scale", minimum=1, maximum=20, step=0.5, value=7.5),
    ],
    outputs=gr.Image(label="Generated Image"),
    title="Stable Diffusion Image Generator"
)

# Launch the Gradio app
interface.launch()
```

### OUTPUT:
![image](https://github.com/user-attachments/assets/09d613be-e371-4d21-a6da-bd9fd5b94c09)

### RESULT:
The prototype successfully generates images based on user-provided prompts and allows interactive parameter adjustments through a user-friendly interface built with Gradio.
