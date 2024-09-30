## Final-Project-Tuwaiq-Generative-AI
# PoemGen: AI Poem Generation Project

This project integrates several generative Artificial Intelligence tasks, including text generation, text-to-speech, translation, and text-to-image, using models from Hugging Face's Transformers library.

The project allows users to generate poems in both Arabic and English based on their input, converts the text to speech, translates Arabic input into English to support text-to-image generation, and produces images that capture the essence of the poem.

## Aim

The aim of this project is to:
1. Generate poems in both Arabic and English based on user input.
2. Convert the generated poems into speech in their respective languages.
3. Translate Arabic poems into English to support image generation.
4. Generate images that visually represent the essence of the input poem.

## Why We Chose These Models

### Text Generation:

- **Arabic Poem Generation**:  
  We chose the [**akhooli/ap2023**](https://huggingface.co/akhooli/ap2023) model for Arabic poem generation because the availability of high-quality Arabic poem generator models is limited, and many existing models lack consistency. This model stood out as the best option to support our idea compared to others.

- **English Poem Generation**:  
  For English poem generation, we selected the [**ashiqabdulkhader/GPT2-Poet**](https://huggingface.co/ashiqabdulkhader/GPT2-Poet) model. Although there is also a lack of high-quality English poem generation models, this one was the best among the available options. While it can generate poems as expected, it sometimes lacks coherence in meaning. However, compared to other models, it provided the most reliable results.

These models are pre-trained for creative text generation, making them ideal for producing meaningful and artistic poems.

  
### Text-to-Speech:

- **Arabic Text-to-Speech**:  
  The [**MBZUAI/speecht5_tts_clartts_ar**](https://huggingface.co/MBZUAI/speecht5_tts_clartts_ar) model was selected for Arabic text-to-speech. After evaluating multiple Text-to-Speech models for Arabic, this one provided superior pronunciation and clarity compared to the others.

- **English Text-to-Speech**:  
  The [**microsoft/speecht5_tts**](https://huggingface.co/microsoft/speecht5_tts) model, developed by Microsoft, was selected for English text-to-speech due to its high-quality pronunciation and clarity. Being from Microsoft, we are confident that this model benefits from state-of-the-art technology and is highly reliable for generating natural and clear speech, making it the best choice for our project.

Both models will enhance the user experience by providing an enjoyable listening experience for the generated poems.


### Text Translation:

Since the image generation model (**runwayml/stable-diffusion-v1-5**) does not support Arabic—primarily focusing on text-to-image generation using English-language prompts—we use the [**Helsinki-NLP/opus-mt-ar-en**](https://huggingface.co/Helsinki-NLP/opus-mt-ar-en) model to translate Arabic poems into English. This ensures that the model can interpret the text effectively and generate accurate images based on the translation. We chose this model as it is one of the most downloaded and highly rated models on Hugging Face specifically for translating Arabic to English.


### Text-to-Image:

The [**runwayml/stable-diffusion-v1-5**](https://huggingface.co/runwayml/stable-diffusion-v1-5) model was chosen for its superior ability to generate detailed and relevant images from textual descriptions. Its advanced capabilities in interpreting prompts enable it to create visually striking and contextually appropriate images based on the provided input.


## Limitations

- **Poem Generation Quality**:  
  The models used to generate poems do not always produce fluent or aesthetically pleasing text. In Arabic, the output is often fragmented and requires significant post-processing to improve readability and coherence.

- **Image Generation from Arabic**:  
  The models that convert Arabic texts into images are limited, and they require a large GPU to function efficiently. Additionally, translation from Arabic to English may not always capture the full poetic nuance or cultural references, which can negatively impact the accuracy and overall quality of the image generation process.

- **Arabic Text-to-Speech Issues**:  
  The Arabic text-to-speech model struggles to complete sentences and often mispronounces or skips certain words. It sometimes stops before finishing a full sentence, resulting in cut-off output. Additionally, it does not handle Arabic text as fluently as the English text-to-speech model.

- **Random Termination in Text Generation**:  
  All text generation models tend to end abruptly and randomly at incomplete points, without concluding the poem naturally. This results in unfinished sentences or thoughts, which diminishes the overall quality of the generated poems.


## Special Measures Taken to Support the Arabic Language

To ensure that Arabic input can be used effectively with models that primarily support English, we implemented a translation step after generating the poem in Arabic. Once the Arabic input is created, it is translated into English using the [**Helsinki-NLP/opus-mt-ar-en**](https://huggingface.co/Helsinki-NLP/opus-mt-ar-en) model. The translated text is then used for image generation, as the image model [**runwayml/stable-diffusion-v1-5**](https://huggingface.co/runwayml/stable-diffusion-v1-5) only accepts English text inputs.

This approach allows us to incorporate Arabic-language inputs into the project while still utilizing powerful image generation models that are limited to English. However, it's important to note that the translation may not always capture the full nuance or cultural context of the original Arabic input, which could influence the accuracy and relevance of the generated image.


## Features

1. **Poem Generation**:
   - Arabic poem generation using the **akhooli/ap2023** model.
   - English poem generation using the **ashiqabdulkhader/GPT2-Poet** model.

2. **Text-to-Speech**:
   - Converts Arabic poems to speech using the **MBZUAI/speecht5_tts_clartts_ar** model.
   - Converts English poems to speech using the **microsoft/speecht5_tts** model.

3. **Translation**:
   - Arabic poems are translated into English using the **Helsinki-NLP/opus-mt-ar-en** model to facilitate image generation.

4. **Text-to-Image**:
   - Generates an image from the translated English input using the **runwayml/stable-diffusion-v1-5** model.

5. **Gradio Interface**:
   - An interactive web interface where users can:
     - Generate poems in Arabic or English.
     - Convert generated poems into speech.
     - Generate an image based on the translated poem.


## Dependencies

To run the project, the following Python packages are required:

- **transformers**
- **gradio**
- **torch**
- **uvicorn** (commented out)
- **datasets**
- **diffusers**

Install these dependencies using pip:

bash
pip install transformers gradio torch datasets diffusers


## Functions

1. *Primary Function: generate_poem*:
   This function receives 2 inputs from the Gradio interface, executes the following functions, and returns 3 outputs:
   - The generated poem.
   - The audio.
   - The image.

2. *Poem Generation Functions: generate_poem_arabic and generate_poem_english*:
   These functions are responsible for generating a poem (text) in Arabic or English, based on the provided text.
   - The `generate_poem_arabic` function generates an Arabic poem.
   - The `generate_poem_english` function generates an English poem.

3. *Audio Functions: text_to_speech_arabic and text_to_speech_english*:
   These functions are responsible for generating audio in Arabic or English, based on the provided text.
   - The `text_to_speech_arabic` function converts Arabic text to speech.
   - The `text_to_speech_english` function converts English text to speech.

4. *Image Function: generate_image_from_poem*:
   This function is responsible for generating an image based on the provided text.

5. *Translation Function: translate_arabic_to_english*:
   This function is responsible for translating the Arabic input to English to be used for the image function, which accepts only English inputs.


## Gradio Interface:

The Gradio interface enables you to choose the language for the poem, either Arabic or English. You can then provide a text (sentence) as a starting point for the poem. The entire poem will be in the context of the provided text (sentence). 

### Expected Results:
1. The generated poem.
2. Audio reading the poem.
3. An image capturing the essence of the poem.

- The Gradio interface uses the primary function `generate_poem`, has predefined examples, features a custom CSS style, and can be launched with `my_model.launch()`.


## Running the Project

To run the project locally, follow these steps:

1. Clone or download the project.
2. Install the required dependencies (refer to the **Dependencies** section).
3. Execute the script:

This will open a Gradio UI where you can select the language (Arabic or English), input a sentence, and generate the following outputs:

- A poem.
- Audio of the generated poem.
- An image.


## Expected Output
Below are the expected outputs for both English and Arabic poem generation, including the generated text, text-to-speech output, translation (if applicable), and the generated image based on the input.

### Example 1: English Poem
#### Input:
json
{
    "dropdown": "English",
    "starter": "The shining sun rises over the calm ocean"
}

#### Output
1. *Generated Poem:*

css
The shining sun rises over the calm ocean,
A golden light that touches every motion.
Waves gently dance under the sky so clear,
A morning melody for all to hear.
Dreams awaken with the break of day,
As sunlight whispers in a soft display.

2. *Text-to-Speech:*
The poem will be converted into English speech using the microsoft/speecht5_tts model, producing natural and clear audio for the generated poem.

3. *Generated Image:* 
An image of a tranquil ocean scene, with the sun rising over calm waters, gently touching the waves. The image will reflect the peaceful and serene environment described in the poem.

### Example 2: Arabic Poem
#### Input:
json

{
    "dropdown": "Arabic",
    "starter": "الورود تتفتح في الربيع"
}


#### Output:
1. *Generated Poem:*

css
الورود تتفتح في الربيع،
بألوان تملأ الفضاء الواسع.
عبيرها يفوح مع النسيم العليل،
ليغني أغنية الفجر الجميل.
الأرض ترتدي ثوب الأزهار،
في موسم الحب والأنوار.


2. *Text-to-Speech:*
 The poem will be converted into Arabic speech using the MBZUAI/speecht5_tts_clartts_ar model. However, due to limitations with the Arabic text-to-speech model, some words may be mispronounced or skipped, and the speech may be cut off before completing the full poem.

3. *Translation for Image Generation:*
Since the image model (CompVis/stable-diffusion-v1-4) only supports English input, the Arabic poem will be translated into English using the Helsinki-NLP/opus-mt-ar-en model:

css
The flowers bloom in spring,
With colors filling the wide space.
Their fragrance spreads with the gentle breeze,
Singing the song of a beautiful dawn.
The earth wears a dress of flowers,
In the season of love and lights.


4. *Generated Image:* 
 An image of blooming flowers in a vibrant spring setting, with colorful blossoms filling the scene. The generated image will reflect the translated poem’s depiction of springtime beauty and nature.
