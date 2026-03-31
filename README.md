# Local Coding Agent

API rate limits are a hard ceiling for solo developers working under financial constraints. This project is an attempt to remove that ceiling entirely by running a capable coding assistant locally — no cloud dependency, no waiting for limits to refresh. I often have to wait for my limits to refresh before I can actually see my ideas as a prototype. Hence to tackle this issue, I am attempting to make use of knowledge distillation to train a smaller model that can run locally on my system to aid with coding while I step away to brainstorm ideas or catchup with the latest advancement in AI technology.

This goal of this project is to create a two agent setup that can run on my local device with a **GTX 1060** with **6GB dedicated VRAM** and **32GB system RAM**. The Hardware constraints are what make the project complex and exciting as a lot of things have to be managed and compromises made to enable the setup to run while ensuring hardware health doesnt degrade too fast.

## Architecture:

*  **Task Master:** **Llama-3.1-8B** will act as the task master to help convert user provided architecture into chunks for the coding model. The Llama-3.x series is considered as being very good at structured reasoning and explanations. That makes it a good candidate for handling user interactions.
*  **Coder:** **Qwen-3.5-9B** will handle the coding tasks that I need handled locally. Since I am distilling it for my use case, this particular model will be trained for android development. By defining the scope of the model it ensures that I get a domain expert that is far better in one domain rather than having multi domain expertise. Since the Qwen-3.5 is considered a multi domain expert that can handle coding in multiple languages, it serves as a good student candidate for distillation for coding related tasks.

## Current Status:

This setup is complex as it has to work around the local restrictions of my ageing hardware, I intend to take some time to ensure that I optimize it for longevity. Currently I am focused on generating high quality seeds to generate synthetic data for the distillation process.
