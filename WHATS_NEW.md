# What's New in AI Toolkit for VS Code Preview

## Version 0.10.5
This version is an incremental release with feature improvements and bug fixes:

- **Tutorials**: Introduce first set of tutorials for common prompt engineering practices. Start one with **CATALOG** > **Tutorials**  
  ![tutorials](https://github.com/user-attachments/assets/240d4034-7731-4975-905d-3241e97293a1)

- **Compare** model responses in Playground  
  ![compare](https://github.com/user-attachments/assets/8144c63a-3f1f-4a5a-948b-916dff07512d)

- **Think Mode** for Claude 3.7 Sonnet model in **Playground** and **Prompt Builder**  
  ![think_in_pb](https://github.com/user-attachments/assets/b42dce7d-2f12-4531-9658-0d1d0079276a)

- **Model Additions**:
  - [QwQ](https://qwenlm.github.io/blog/qwq-32b/) via Ollama: Thinking and reasoning model of the Qwen series.
  - [GPT-4.5](https://openai.com/index/introducing-gpt-4-5/) from OpenAI: A general-purpose LLM targeted at providing more natural, fluid interactions that are humanlike.
  - [DeepSeek v3](https://github.blog/changelog/2025-03-07-deepseek-v3-is-now-generally-available-in-github-models/) via GitHub: Strong performance in coding, math and reasoning tasks.

- Incremental feature enhancements:
  - **Playground** improvements:
    - Copy model response
    - Regenerate response with the same or a different model
  - **Model Catalog** improvements:
    - Quick access to `Claude 3.7 Sonnet`, `GPT-4.5` and `QwQ` model via `Popular Models`
    - Filter models by features such as Web Search, Attachment and Structured Outputs

## Version 0.10.2
This version is an incremental release with feature improvements and bug fixes:
- More AI models are supported:
  - [Anthropic Claude 3.7 Sonnet](https://www.anthropic.com/news/claude-3-7-sonnet) model (excluding `extended thinking mode`)
  - [Phi-4-mini-instruct](https://github.com/marketplace/models/azureml/Phi-4-mini-instruct)
  - [Phi-4-multimodal-instruct](https://github.com/marketplace/models/azureml/Phi-4-multimodal-instruct)
- Playground improvements:
  - Add web search support for models that are capable doing it (e.g., Gemini 2.0)
  - Add support to extract file content (text, PDF, JSON...) for models lacking native attachment support
  - Recommend conversation starters when opening Playground
  - Add default pre-selected model when opening Playground 
- Prompt Builder improvement:
  - Improve the UI to help new user get started 

## Version 0.10.1
This is an incremental release with feature enhancements and bug fixes:
- Improved model catalog experiences:
  - Streamline Ollama lifecycle (download, load, multi quantization in one card)
  - Enable access of popular Ollama models in model catalog
  - Categorize models for easy model discovery
  - Search models
- Playground improvements:
  - Auto naming the new playground/prompt
  - New playground carries over the last model selection & preference
- UI improvements:
  - Group my models by host in tree view
  - Support streaming response in Prompt Builder

## Version 0.10.0
This is a major milestone release with new feature additions and updates:
  - More AI Models:
    - GitHub hosted o3-mini model
    - Google Gemini 2.0 models
    - Anthropic Claude 3.5 Haiku model
    - Nvidia hosted NIM models
  - Prompt Builder:
    - Allow easy prompt creating / editing / testing
    - Generate prompt using AI models
    - Support structured output
    - Generate ready code to interact prompts with AI model 
  - Playground Improvements:
    - Refined Deepseek-R1 thought UI
    - Refined Markdown and Latex rendering from model output
  - Bulk Run Improvements:
    - Generate dataset using AI models
    - Support structured output
  - Custom Evaluator:
    - Custom evaluator from Python codes
    - Custom evaluator from LLM prompt
    

## Version 0.8.6
This is a patch version to the major milestone release 0.8.0 with feature improvement:
  - Support DeepSeek R1 Distilled (qwen 1.5B) NPU Model for Copilot+ PCs
    - Supported SKU:
      - Qualcomm Snapdragon X   
      - Intel Core Ultra 200V - coming soon

## Version 0.8.5
This is a patch version to the major milestone release 0.8.0 with feature improvement:
  - Support DeepSeek-R1 Model

## Version 0.8.3
This is a patch version to the major milestone release 0.8.0 with some feature improvements and bug fixes:
   - Support chat history management in Playground.
   - Support prompt templating with variable in Bulk Run.

## Version 0.8.0
This is a milestone release with core feature additions and improvements
  - Support Bulk Run that user can run any prompts from imported datasets or run in full bulk 
  - Evaluate a dataset with a set of pre-defined popular evaluators
  - Incremental UI/UX improvements and bug fixes

## Version 0.6.2
This is a patch version to the major milestone release v0.6.0, with some highly demanded feature improvements and bug fixes:
  - Support Ollama models from more UI entries with improved doc
  - Support Intel-based Mac (ONNX models support coming next)
  - Support attachment for selected GitHub multi-modal models: (Llama-3.2-11B-Vision-Instruct / Llama-3.2-90B-Vision-Instruct / gpt-4o / gpt-4o-mini / Phi-3.5-vision-instruct)
  - Added direct entry of developer documentation from AI Toolkit treeview 
  - Support responsive UI for attachments
  - Count the total tokens used in each playground conversation
  - Multiple bug fixes

## Version 0.6.0
This is a major milestone release with significant additions of features and resources.

  - Most popular generative AI models on market are now supported:
    - GitHub models
    - ONNX optimized models that run on local CPU (including Windows optimized Small Language Models like Phi family)
    - Anthropic Claude Models
    - Google Gemini Models
    - Meta Llama Models
    - And more
  - Bring your own model as remote model.
  - Quickly discover a model by comprehensive filters and detailed model card in model catalog.
  - Inference test and chat with a model in Playground with improved experience.
  - Attachment in playground chat is now supported for multi-modal models.
  - Further improved get started guide.
    
With these features, developers can easily get start and explore any popular genAI model from a single tool. 

## Version 0.5.0
0.5.x are pre-released versions with major improvements on model selections and playground experience.

  - GitHub AI models are now supported (Requiring proper GitHub License).
  - Filters are added on model catalog.
  - Models run in AI Toolkit can now be edited and deleted.
  - In-code evaluation sample published.
  - Get started guide with a simple Small Language Model is now available for new users.

## Version 0.4.0
This version adds the key support for Mac users and AI PC users:

  - Mac-Silicon (M1, M2, etc.) is now supported, Mac-Intel is not yet supported.
  - Mac doesn't have NVidia GPUs, so we hide local finetuning entry for Mac version AI Toolkit.
  - AI PC (Copilot PC) is supported.

We are excited to announce another important feature:
    
  - Remote inference test in playground is now supported, through connecting to remote model endpoint. Both UI and Command Palette have entry for connecting to a remote model endpoint.

## Version 0.3.0
We are excited to announce that Windows AI Studio has been renamed to AI Toolkit for Visual Studio Code, to expand its support of broader range of AI models, covering major scenarios for AI Engineers or App Developers to develop intelligent app with AI models. With this preview version 0.3.0, we are introducing many new features and enhancements:

**Redesigned UI**

We have made significant UI design updates to improve the visuals and user experiences.

**Model catalog**

The new Model catalog helps developer to easily discover and download a supported text generation AI model to local environment. In this version we support:

   - Phi-2 
   - Phi-3-mini with a variety of sizes and CPU/GPU supports
   - mistral-7b

**Playground for inference**

Downloaded models are ready to test inference with newly enhanced UI on local environment, with proper CPU or GPU support.

**Fine-tune model locally**

If developer's local environment has GPU support, model fine-tuning can be performed on local machine, after passing the pre-requisite test. Current supported models for fine-tuning:

   - meta-llama/Llama-2-7b
   - microsoft/phi-2
   - mistralai/Mistral-7B
   - microsoft/phi-1_5
   - microsoft/Phi-3-mini-4k-instruct
   - HuggingFaceH4/zephyr-7b-beta

**Fine-tune model remotely**

This is a preview feature that can be enabled from Visual Studio Code settings. For developers who have access to Azure cloud resources with GPU, they can perform the fine-tune jobs on Azure Container App remotely from Visual Studio Code.

**Deploy models**

Fine-tuned models can be deployed to a provisioned Azure Container App for testing or integrating.

**Coming soon**

We are actively adding support for e2e development needs around AI app and AI models.
   - Add more models for inference and fine-tune support.
   - Enable batch test and auto-evaluation of AI models.
   - Streamlined development and test support for intelligent apps with AI models.
   - Enhacing RAG and Prompt engineering support for developing and testing AI apps with AI models.


## Version 0.2.4

The selection of Windows optimized models is now available in Windows AI Studio. You can download those models from Hugging Face and GitHub and use in your Windows applications.

## Version 0.2.3

This version adds a prerequisite check, ensuring that VS Code does not have a remote connection.

## Version 0.2.2

This version fixes a few bugs, including -

- Conda environment fails to install in certain cases.

## Version 0.2.0

We are excited to introduce Windows AI Studio Preview version 0.2.0, which brings several new features and enhancements to simplify generative AI app development and local fine-tuning. Here's what's new:

### New Features and Enhancements

1. **Model Catalog**
   - Windows AI Studio now offers an expanded model catalog powered by Azure ML and Hugging Face. In this release we offer 3 text generation AI models ready to be configured for fine-tuning and inferencing locally.

        - Meta/Llama-2-7b
        - Microsoft/phi-1.5
        - Microsoft/phi-2
        - mistralai/Mistral-7B
        - HuggingFaceH4/zephyr-7b-beta

2. **Prerequisites Check**
   - Before installing Windows AI Studio, the new Prerequisites Check ensures that your system meets the necessary requirements, such as NVIDIA GPUs with minimun 8GB VRAM and recommended 16GB+ VRAM with a compatible WSL Ubuntu distribution installed. This ensures a smooth installation process.

   - Expected times for different GPUs on default Dataset

      | GPU             | Dataset | Time    |
      |-----------------|---------|---------|
      | RTX 3080 Ti Mobile | Default | 52 mins |
      | RTX 4090 | Default |  42 mins |
      | RTX A6000 | Default | 35 mins|
      | RTX ADA5000 Mobile | Default | 49 mins |
      | RTX A6000 ADA | Default | 32 min |
      

3. **Model Fine-tuning**
   - Fine-tuning AI models has never been easier. With Windows AI Studio, you can select a model from the catalog and fine-tune it locally using QLoRA. You can get started with your GitHub account.

4. **Customizable Settings**
   - When fine-tuning a model, you have the flexibility to adjust various settings, including data types, dropout probabilities, batch sizes, and more. Customize the parameters to optimize the fine-tuning process for your specific scenario.

5. **Windows Optimized Models**
   - Discover a collection of publicly available AI models already optimized for Windows. These models are sourced from different locations, including Hugging Face and GitHub, and are ready for download and use in your Windows applications.

6. **Q&A Page**
   - To address common issues and provide resolutions, we have introduced a [FAQ page](https://aka.ms/ai-toolkit/doc-faq). You can refer to this page for solutions to frequently encountered problems.

7. Please see our [documentation](https://aka.ms/ai-toolkit/doc-overview) for more in depth information and walkthrouhgs of the tool.

### Coming Soon

While the current release brings many exciting features, we are also working on the following additions:

- **RAG Project**: Stay tuned for the upcoming RAG Project feature, which will further enhance your AI development capabilities.

- **Phi-2 Model Playground**: Explore the Phi-2 Model Playground, a new feature that will provide an opportunity of using Phi-2 locally directly from the tool.
