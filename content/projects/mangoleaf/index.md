---
title: Mango Leaf Classifier
draft: false
series_order: 2
---

Mango-Leaf is an innovative platform which uses Artificial Intelligence to detect if a mango leave is either healthy or showing signs of disease. It consist of two main parts: the first one is a deep learning model wich achieved a remarkable 98% accuracy in disease classification. The second part consists of a connection to a LLM (GPT 3.5) to interpret the diagnosis and signal possible causes for the diseas as well as recomendations to treat the plant.

<video controls>
  <source src="multimedia/mango-leaf-video.mp4" type="video/mp4">
</video>


### Technologies Used:

- **TensorFlow**: The machine learning framework that powers the image classification model.
- **Python**: The programming language used for developing the classifier and the FastAPI application.
- **NumPy**: A library for numerical operations, essential for data manipulation in the model.
- **FastAPI**: A modern, fast (high-performance), web framework for building APIs.
- **OpenAI**: An API which allows for comunication with OpenAI LLMs like GPT 3.5.
- **Streamlit**: A Python library which allows for UI creation focusing on AI projects.
- **Docker**: Containerization technology for packaging the application and its dependencies.


### Project Components:

1. **Dataset**: The model is trained on a dataset obtained from [kaggle](https://www.kaggle.com/datasets/warcoder/mango-leaf-disease-dataset/data), it contains images of mango leaves both healthy and diseased. To manage all these images we used the numpy libraries functions to clean the dataset. In order to prepare it for the training we used the split functions from the scikit-learn library. 

2. **TensorFlow Model**: We leverage the power of TensorFlow to create a deep learning model using the ResNet50V2 Base Model. Then we construct a custom model using a Sequential model from the keras module with the following layers:
    - The pre-trained ResNet50V2 model.
    - BatchNormalization layer.
    - Dense layer with leaky ReLU activation, He normal initialization, and 512 neurons.
    - Another BatchNormalization layer.
    - Dropout layer with a dropout rate of 30%.
    - Dense layer with leaky ReLU activation, He normal initialization, and 128 neurons.
    - Another BatchNormalization layer.
    - Another Dropout layer.
    - Dense layer with softmax activation, Glorot uniform initialization, and 8 neurons (assuming it’s a classification task with 8 classes).

3. **BackEnd**: We use FastAPI to create a simple post endpoint to interact with the model. The request contains the image of a mango leaf, and the response returns the models prediction. This prediction is then passed to a prompt, which is then sent to GPT 3.5 with the help of the OpenAI python module. GPT 3.5 then returns possible causes for the disease as well as recomendations to treat it.

4. **FrontEnd**: Finally we create a simple UI using streamlit. Streamlit allows us to easily implement image upload functinalities as well as a chat interface to interact with GPT 3.5