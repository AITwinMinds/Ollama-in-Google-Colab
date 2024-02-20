# Ollama in Google Colab

This repository provides instructions and code snippets for using [Ollama](https://github.com/ollama/ollama) in Google Colab notebooks.

## Installation

To install Ollama in your Colab environment, follow these steps:

1. Run the following command in a code cell to install the required dependencies:

    ```bash
    ! sudo apt-get install -y pciutils
    ```

2. Run the installation script provided by Ollama:

    ```bash
    ! curl https://ollama.ai/install.sh | sh
    ```

3. Import the necessary libraries and define the Ollama function:

    ```python
    import os
    import threading
    import subprocess
    import requests
    import json

    def ollama():
        os.environ['OLLAMA_HOST'] = '0.0.0.0:11434'
        os.environ['OLLAMA_ORIGINS'] = '*'
        subprocess.Popen(["ollama", "serve"])
    ```

## Usage

Once Ollama is installed, you can use it in your Colab notebook as follows:

1. Start the Ollama server by running the following code:

    ```python
    ollama_thread = threading.Thread(target=ollama)
    ollama_thread.start()
    ```

2. Run the Ollama model of your choice. For example, to use the `mistral` model, execute:

    ```python
    ! ollama run mistral
    ```

    After seeing this message `Send a message (/? for help)`, stop the execution and proceed to the next step.

3. Now you need to start the Ollama server again by running the following code:

    ```python
    ollama_thread = threading.Thread(target=ollama)
    ollama_thread.start()
    ```

4. Now, you can interact with Ollama by sending prompts and receiving responses. Here's an example:

    ```python
    prompt = """
    What is AI?
    Can you explain in three paragraphs?
    """
    ```

5. Then, run the following code to receive the response based on your prompt. Here, `stream` is set to `False`, but you can also consider a streaming approach for continuous response printing:

    ```python
    url = 'http://localhost:11434/api/chat'
    payload = {
        "model": "mistral",
        "temperature": 0.6,
        "stream": False,
        "messages": [
            {"role": "system", "content": "You are an AI assistant!"},
            {"role": "user", "content": prompt}
        ]
    }

    response = requests.post(url, json=payload)
    message_str = response.content.decode('utf-8')
    message_dict = json.loads(message_str)
    print(message_dict['message']['content'])
    ```

This will send the prompt to the Ollama model and print its response.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support Us

If you find it helpful, consider supporting us in the following ways:

- ⭐ Star this repository on [GitHub](https://github.com/AITwinMinds/Ollama-in-Google-Colab).
  
- 🐦 Follow us on X (Twitter): [@AITwinMinds](https://twitter.com/AITwinMinds)

- 📣 Join our Telegram Channel: [AITwinMinds](https://t.me/AITwinMinds) for discussions and announcements.

- 🎥 Subscribe to our YouTube Channel: [AITwinMinds](https://www.youtube.com/@AITwinMinds) for video tutorials and updates.

- 📸 Follow us on Instagram: [@AITwinMinds](https://www.instagram.com/AITwinMinds)

Don't forget to share it with your friends!

## Contact

For any inquiries, please contact us at [AITwinMinds@gmail.com](mailto:AITwinMinds@gmail.com).


