# LINA - Linguistic Intelligent Navigation Assistant

*LINA stands for **Linguistic Intelligent Navigation Assistant***.

> **Note:** This repository is a fork of Joan's LINA for a Master 2 project. The original repository can be found here:  
> [https://gitlab.com/joan.g.francois/lina.git](https://gitlab.com/joan.g.francois/lina.git)

## Overview

LINA is a multi-modal document search engine that leverages both text and voice interfaces to search within a large textual library. The application supports various search functionalities—including keyword search, regex-based advanced search, and integrated correction features—and also provides an in-app reader for displaying full text documents. The system uses machine learning models for subject and type classification, value estimation, and speaker identification, and employs a flexible plugin architecture to generate responses.

## Architecture and Modules

### Core Modules

- **app.py**  
  Implements core functions for analyzing text input. This module loads machine learning models to classify subjects, types, and values from a given sentence. It also selects appropriate response plugins based on the analysis.

- **models.py**  
  Defines and trains various neural network models using TFLearn. The models include:
  - Subject classification model
  - Type classification model
  - Value estimation model
  - Speaker identification model

- **tools.py**  
  Provides utility functions for natural language processing tasks such as tokenization, stemming (using NLTK's FrenchStemmer), bag-of-words generation, and data loading from JSON files. These functions support both training and inference processes.

### Plugin System

- **pluginDefault.py** and **pluginFactory.py**  
  Implement a flexible plugin system for generating responses. The default plugin handles general queries, while specialized plugins (e.g., for alarm or remote commands) can be integrated to extend functionality.

### Voice Interface

- **microphone.py**  
  Implements real-time speech recognition using the Vosk library. It captures audio input, converts it to text, and processes it through the analysis pipeline. Speaker recognition is also performed to tailor responses based on the identified user.

- **speaker.py**  
  Handles audio file processing for training and evaluating the speaker identification model, facilitating improved voice command handling.

## Functionalities

- **Search Capabilities:**
  - **Keyword Search:** Returns documents containing the specified keyword.
  - **Advanced Regex Search:** Returns documents matching a provided regular expression pattern, with options to search through indexing data or full text (noting that the latter may impact performance).
  - **Levenshtein Correction:** Utilizes the Levenshtein distance algorithm to suggest alternative search terms in cases of spelling errors, enhancing overall search accuracy.

- **Result Ranking:**
  Documents are ranked based on relevance, considering criteria such as:
  - Frequency of keyword occurrences.
  - Centrality measures derived from a Jaccard graph (using metrics like closeness, betweenness, or pagerank).

- **Integrated Book Reader:**
  Provides a built-in reader mode to display the full text of selected documents, ensuring a seamless reading experience on both web and mobile platforms.

- **Voice Commands and Speaker Recognition:**
  Supports real-time voice interaction, with capabilities for both speech-to-text conversion and speaker identification to personalize responses.

## Installation and Setup

### Prerequisites

- Python 3.x
- Required Python libraries: TensorFlow, TFLearn, NLTK, Vosk, pyttsx3, and others as listed in `requirements.txt`
- Vosk models should be placed in the appropriate directories (e.g., `model` for speech recognition, `model-spk` for speaker recognition)
- JSON training data should be available in the `training_data` and `plugins` directories

### Setup Steps

1. **Install Dependencies:**  
   Install all required Python packages using your preferred package manager.

2. **Prepare Training Data:**  
   Ensure that JSON files for training (both for general language processing and plugin-specific intents) are correctly placed in the `training_data` and `plugins` folders.

3. **Train Models:**  
   - Launch `models.py` to train the AI models.
   - Launch `speaker.py` to train the speaker identification model.

4. **Run the Application:**  
   - Launch `app.py` to boot the AI for text-based search functionality.
   - Launch `microphone.py` for voice-based interaction.

## Usage

1. **Training:**  
   Run `models.py` to train the AI models with the available training data.

2. **Booting the AI:**  
   Run `app.py` to start the text-based search engine.

3. **Voice Interaction:**  
   Run `microphone.py` to engage with LINA via voice commands.

Enjoy using LINA!
