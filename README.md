# OpenWeaver_GenerativeAI_Text_To_Image
This repository contains the code and resources related to a text-to-image generative AI internship. The goal of this internship is to explore and develop techniques for generating realistic images based on textual descriptions using generative AI models.
# Text to Image Generation
To perform text-to-image generation in Python using the OpenAI library, you can utilize the CLIP (Contrastive Language-Image Pretraining) model and an image generation model like DALL-E. Here's an example:

# Importing Necessary Libraries
import gradio as gr
import openai
#Add the access key generated from your OpenAI account
openai.api_key = "YourAPI"

# Creating our Assistant
def chatgpt_api(input_text):
    messages = [
        {"role": "system", "content": "Hello I'm Jarvis Singh, your personal Assistant"},
        {"role": "user", "content": input_text}
    ]
    
    chat_completion = openai.ChatCompletion.create(
        model="gpt-3.5-turbo", messages=messages
    )
    
    reply = chat_completion.choices[0].message.content
    return reply
# Image Generator (DALL-E)
def dall_e_api(dalle_prompt):
    dalle_response = openai.Image.create(
        prompt=dalle_prompt,
        size="512x512"
    )
    image_url = dalle_response['data'][0]['url']
    return image_url
# Generate Image from Text
def generate_image(input_text):
    dalle_prompt = chatgpt_api(input_text)
    image_url = dall_e_api(dalle_prompt)
    return image_url
input_text = gr.inputs.Textbox(label="Input Text")
output_image = gr.outputs.Image(type="pil", label="Generated Image")

# Gradio Interface
image_generation_interface = gr.Interface(
    fn=generate_image,
    inputs=input_text,
    outputs=output_image,
    title="Welcome To Abhishek's Text to Image Generation",
    description="Enter your imagination"
)
image_generation_interface.launch(debug=True)
Running on local URL:  http://127.0.0.1:7860

To create a public link, set `share=True` in `launch()`.

 
