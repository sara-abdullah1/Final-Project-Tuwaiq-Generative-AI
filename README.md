# Final-Project-Tuwaiq-Generative-AI
# PoemGen: AI Poetry Generation Project

This project integrates several generative Artificial Intelligence tasks, including text generation, text-to-speech, translation, and text-to-image, using models from Hugging Face's Transformers library.

The project allows users to generate poems in both Arabic and English based on their input, converts the text to speech, translates Arabic input into English to support text-to-image generation, and produces images that capture the essence of the poem.

## Aim

The aim of this project is to:
1. Automatically generate poems in both Arabic and English.
2. Convert the generated poems to speech in their respective languages.
3. Translate Arabic poems into English for image generation.
4. Generate images that reflect the input sentence of the poems based on the English translation.

## Why We Chose These Models

- *Text Generation*: 
We chose the akhooli/ap2023 model for Arabic poem generation and the ashiqabdulkhader/GPT2-Poet model for English. These models are pre-trained for creative text generation, making them ideal for producing meaningful and artistic poems.
  
- *Text-to-Speech (TTS)*: 
The MBZUAI/speecht5_tts_clartts_ar model was selected for Arabic text-to-speech, and microsoft/speecht5_tts for English. Both models are highly accurate in producing natural-sounding speech, which enhances the user experience of listening to the generated poems.

- *Translation*: 
Since the image generation model (CompVis/stable-diffusion-v1-4) does not support Arabic, we use the Helsinki-NLP/opus-mt-ar-en model to translate Arabic poems into English. This ensures that the model can interpret the text effectively and generate accurate images based on the translation.

- *Image Generation*: 
The runwayml/stable-diffusion-v1-5 model was chosen for its superior ability to generate detailed and relevant images from textual descriptions. By translating Arabic poems into English, we ensure that the model can interpret the meaning effectively and generate accurate visuals.

## Limitations
- *Poem Generation Quality*: 
The models used to generate poems do not always produce fluent or aesthetically pleasing text. In Arabic, the output is often broken and requires significant post-processing to clean up and enhance the text's readability and coherence.
  
- *Image Generation from Arabic*: 
The models that convert Arabic texts into images are few, and they require a large GPU to function efficiently. Additionally, the translation from Arabic to English may not always capture the full poetic nuance or cultural references, which can negatively impact the accuracy and overall quality of the image generation process.

- *Arabic Text-to-Speech Issues*: The Arabic text-to-speech model struggles to complete sentences and often mispronounces or entirely skips certain words. Sometimes stop before completing the full sentence, leaving the output cut off. It does not handle Arabic text as fluently as the English text-to-speech model.

- *Random Termination in Text Generation*: All text generation models tend to end abruptly and randomly at incomplete points, without concluding the poem naturally. This results in unfinished sentences or thoughts, which diminishes the quality of the generated poems.

## Special Measures Taken to Support the Arabic Language

To ensure that Arabic poems can be used effectively with models that primarily support English, we implemented a translation step after generating the poem in Arabic. Once the Arabic poem is created, it is translated into English using the Helsinki-NLP/opus-mt-ar-en model. The translated text is then used for image generation, as the image model (CompVis/stable-diffusion-v1-4) only accepts English text inputs. 

This approach allows us to incorporate Arabic-language poems into the project, while still utilizing powerful image generation models that are limited to English. However, it's important to note that the translation may not always capture the full nuance or cultural context of the original Arabic poem, which could influence the accuracy and relevance of the generated image.

## Features

1. *Poem Generation*:
   - Arabic poem generation using the akhooli/ap2023 model.
   - English poem generation using the ashiqabdulkhader/GPT2-Poet model.

2. *Text-to-Speech (TTS)*:
   - Converts Arabic poems to speech using the MBZUAI/speecht5_tts_clartts_ar model.
   - Converts English poems to speech using the microsoft/speecht5_tts model.

3. *Translation*:
   - Arabic poems are translated into English using the Helsinki-NLP/opus-mt-ar-en model to facilitate image generation.

4. *Text-to-Image*:
   - Generates an image from the translated English poem using the CompVis/stable-diffusion-v1-4 model.

5. *Gradio Interface*:
   - An interactive web interface where users can:
     - Generate poems in Arabic or English.
     - Convert generated poems into speech (TTS).
     - Translate Arabic poems into English.
     - Generate an image based on the translated poem.

## Dependencies

To run the project, the following Python packages are required:

- transformers
- gradio
- torch
- uvicorn
- soundfile
- datasets
- diffusers

Install these dependencies using pip:

bash
pip install transformers gradio torch uvicorn soundfile datasets diffusers


## Funcations

1. *Poem Generation*:

- The generate_poem function generates a poem or text based on a provided sentence.

2. *Text-to-Speech (TTS)*:

- The text_to_speech_arabic function converts Arabic text to speech.
- The text_to_speech_english function converts English text to speech.

4. *Gradio Interface*:
- The generate_image_from_poem function creates an image based on the input poem.

### 4- Gradio Interface:

- The Gradio interface can be launched with my_model.launch().

## Running the Project
To run the project locally, use the following steps:
    1- Clone or download the project.
    2- Install the required dependencies.
    3- Execute the script:

This will open a Gradio UI where you can select the language (Arabic or English), input a sentence, and generate the following outputs:

- A poem.
- Audio of the generated poem (TTS).
- An image based on the generated poem.

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
