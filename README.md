# Local LLM Chatbot Demonstration

This project demonstrates the use of local large language models (LLMs) as chatbots, leveraging [LM Studio](https://github.com/LMStudio/LM-Studio) to host and interact with the model. The implementation is showcased using Jupyter notebooks, providing a seamless and interactive environment for development and testing.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Example](#example)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

To set up LM Studio, follow these steps:

1. **Visit the Official LM Studio Website**  
   Navigate to the [LM Studio Website](https://lmstudio.ai/) for the latest releases and installation instructions.

2. **Download the Latest Release**  
   Download and install LM Studio depending on the OS.

3. **Loading a LLM locally**  
   After installation, download the LLM and start the local server.

For more detailed information and troubleshooting, refer to the [official documentation](https://github.com/LMStudio/LM-Studio/wiki).

## Installation

To set up the environment, ensure you have the necessary Python packages installed. You can install them using the following commands:

```python
%%capture
!pip install llama-index-core llama-index llama-index-llms-lmstudio
```

Additionally, the `nest_asyncio` package is used to enable asynchronous capabilities within the Jupyter notebook environment:

```python
import nest_asyncio
nest_asyncio.apply()
```

## Usage

The project uses the LMStudio class from the llama_index.llms.lmstudio package to interface with the locally hosted model. You can specify the model's configuration and base URL to connect to the LM Studio server.

Here is an example of how to set up and use the model:

```python
from llama_index.llms.lmstudio import LMStudio
from llama_index.core.base.llms.types import ChatMessage, MessageRole

llm = LMStudio(
    model_name="lmstudio-community/Meta-Llama-3.1-8B-Instruct-GGUF",
    base_url="http://localhost:1234/v1",
    temperature=0.7,
)

messages = [
    ChatMessage(
        role=MessageRole.SYSTEM,
        content="You are an expert AI assistant. Help the User with their queries.",
    ),
    ChatMessage(
        role=MessageRole.USER,
        content="What is the significance of the number 42?",
    ),
]

response = llm.stream_chat(messages=messages)
for r in response:
    print(r.delta, end="")
```

## Example

To demonstrate the functionality, we initiate a conversation where the user asks about the significance of the number 42. The system responds by drawing from the model's knowledge base, providing a comprehensive answer.

## Contributing

Contributions are welcome! If you'd like to contribute, please fork the repository and create a pull request with your changes. Ensure that your contributions align with the project's goals and adhere to the coding standards.

## License

This project is licensed under the MIT License.
