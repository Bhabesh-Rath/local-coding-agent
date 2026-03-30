# Decisions:

## Hardware Constraints:
*  7 year old gaming laptop - well maintained
*  GTX 1060 - 6GB dedicated VRAM
*  32GB RAM
*  The system has to work for at least another two to three years

## Model Training:

### Overall structure:
*  **Professor Model:** Claude Sonnet 4.6 for seed generation.
*  **Test Taker/ Master Model:** DeepSeek-R1 for generating synthetic data.
*  **Base Student:** Qwen-3.5-9B

The entire distillation process can be visualized as the professor(Claude) setting a test for the industry expert(DeepSeek) to take. The industry expert provides well reasoned and detailed answers to the questions. The answers are then checked by the professor to check if the expert maintained sanity throughout the test. Finally these answers are compiled as a highly detailed book for the student(Qwen) to learn from. Once the student covers the book thoroughly, it graduates and is ready to work in the field.

This process ensures that the quality of the synthetic data used to train the model is of a very high standard where it won't face any issues when trying to tackle real world tasks.

### Model Selection:

*  **Claude Sonnet-4.6:** The professor model.
  *  Advantages: The model is really good at handling edge cases and tricky problems given it's high SWE-bench score. It can also get information form the web allowing it to get information on issues, both common and rare as well as best industry practices.
  *  Disadvantages: Under financial constraints, the rate limits are reached relatively fast making the work of seed generation extremely slow.

  Since the model could promise higher quality seeds, the decision was made to accept the extra time it would take as an unavoidable price.

*  **DeepSeek-R1:** The expert model.
  *  Advantages: The model is high performing over a range of tasks. It also has the capability to generate Chain-of-Thought and self correct.
  *  Disadvantage: DeepSeek R1 is a huge model which once again causes a similar issue under financial constraints. It sometimes mixes languages and is sensitive to prompting.

  Since the model can generate CoT, that data can be used to allow a smaller model to punch above it's weight category. This the decision was made to stick with the model and work around the disadvantages.

*  **Qwen-3.5_9B:** The student model.
  *  Advantages: State of the art model that uses hybrid architecture (Gated Delta Networks + Attention) that allows it to outperform much larger models. The size makes it highly capable for local use.
  *  Disadvantages: The low parameter count means reduced logic depth. It has been shown that these models often use distributed reasoning which can increase the number of failure modes. There is also the chance of long-context drift and issues with adherance to complex constraints and nuances. It would also be relatively rigid compared to bigger models.

The model being SOTA and relatively high performing makes it a good candidate for the student model application. As things stand, I am actively looking for a workaround to deal with these disadvantages.
