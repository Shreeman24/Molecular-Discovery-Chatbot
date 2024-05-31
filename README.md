# Molecular Discovery Chatbot

## Project Demo: tinyurl.com/MolecularDiscoveryChatbot

The Molecular Discovery Chatbot employs low-cost open-source libraries to build and deploy an interactive front-end web chatbot with a specialized back-end Large Language model (LLM) for extracting and discovering chemical and biomedical knowledge about small molecules and proteins. The chatbot, a conversational artificial intelligence (AI) agent, integrates Natural Language Processing (NLP) techniques including (1) data pipelines (collection, loading, preprocessing, and tokenization), (2) fine-tuning a pre-trained LLM despite limited data and limited GPU computing, (3) data retrieval and management, and (4) deploying the resulting LLMs in local or cloud computing infrastructure (Google Colab). Compared to generic LLMs for natural languages, our specialized LLMs are for 1-dimensional “texts” of small molecules, such as SMILES strings, and those for proteins, such as amino-acid sequences.  Besides facilitating the public to acquire personalized knowledge about molecules of therapeutic value, the chatbot system promotes knowledge discovery for researchers in drug discovery and disease treatment.  By incorporating molecular texts with binding affinity data between small-molecule drug candidates and protein targets, the chatbot system is developed and benchmarked for its potential to suggest molecular modifications when prompted by user inputs.

![Subsystem Diagram](https://github.com/Shreeman24/Molecular-Discovery-Chatbot/blob/main/ECEN%20403%20Subsystem%20Diagram.png)

The online database is curated with PDF information of functional group properties, educational assessments to test model performance, and binding affinity data from DeepAffinity. They were all further cleaned and pre-processed and fed into other subsystems.

The tokenizer subsystem performs text-level and SMILES tokenization of the paired text-sequence data using Sentence Transformers in LangChain and FAISS to allow efficient vector-based similarity search of text. It also supports SMILES tokenization at atom-level and fragment-level and subsequently performs molecular editing. 

On the chatbot page, an educational user can request information on the chemical property of small molecules while an advanced research user can request input SMILES sequences to be modified based on binding affinity values. Using the SMILES sequence, the tokenizer subsystem performs molecular editing while the LLM subsystem undergoes prompt engineering to format the output for the user. 

The HuggingFace Llama2 model in the LLM subsystem generates responses through sequential communication implemented with a conversation retrieval chain. Using the SMILES and PDB output, the visualization subsystem can generate 2D structure and 3D fold visualizations demonstrating the modified small molecule. On the chatbot, the user can navigate between the database and the chatbot page of the front-end interface.

The user may request to export the newly created small molecule information or generate further explanation of the modifications. The former case exports the chat history of the current session. It adds the small molecule structure and textual information about its modifications to the back-end Google Firebase database system. The database can be retrieved to display the most recently edited small molecule entries on the chatbot interface. The latter case involves the user asking a follow-up question to explain output responses further. This pushes all conversational data through a conversational retrieval chain and feeds it as an input to the LLM. Hence, the model generates future responses based on current and previous inputs, tokenizing them, and creates a response that aims to answer the user’s query.

The whole subsystem is deployed and incrementally migrated from the CPU on the local Device to leveraging GPU resources on Google Colab for parallelized and accelerated implementation of every subsystem.

## Requirements
*    Have at least 15GB storage in Google Drive to store the model
*    Navigate to Llama2 Models link below to download the q2_K and q4_0 models
*    Upload all the model binary files and data files from the repo onto your Google Drive
*    Have access to Colab Pro or access to T4 GPU on Google Colab for fine-tuning. You do not need Colab Pro to execute (Overall_Working)_Molecular_Discovery_Chatbot.ipynb.
*    Change the file paths from '/content/drive/MyDrive/...' to the file paths of the models and data for all files

## How to run?
*    Navigate to (Overall_Working)_Molecular_Discovery_Chatbot.ipynb to execute the chatbot
*    To fine-tune LLM using QLoRA, execute (Fine_Tuning)_Molecular_Discovery_Chatbot.ipynb on T4 GPU with High RAM

Llama2 Models: https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGML/tree/main

Sponsor Lab Github: https://github.com/Shen-Lab/DeepAffinity/
