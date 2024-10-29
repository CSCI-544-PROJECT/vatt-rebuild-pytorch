# VATT - Long-Form Audio and Text Model

This project is an implementation of the **VATT (Video-Audio-Text Transformer)** model, adapted specifically for long-form audio and text data. The goal is to explore whether VATT can be used effectively on long-format data by focusing on extended audio samples and text transcripts, omitting the video component from the original implementation.

## Documentation on design choices

[Goto the documentation repo for in-depth discussion.](https://github.com/CSCI-544-PROJECT/documentation)

## Dataset

To train this model, we use the **TED-LIUM dataset** containing audio files of TED talks along with their transcripts. The dataset can be downloaded from the following link:

[Download TED-LIUM Dataset](https://drive.google.com/drive/folders/15_aBPLIIEGZJBZrnwDPQ-DfsqKSRxS-J?usp=sharing)

## Project Structure

```
├── audio_files/                # Directory containing audio files in .wav format
├── transcript_files/           # Directory containing transcript files in .stm format
├── vatt-rebuild-pytorch.ipynb  # Jupyter notebook with code for the project
├── README.md                   # Project documentation
└── requirements.txt            # Python dependencies
```

## Setup and Installation

### Step 1: Install Dependencies

To install the required libraries, use the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

> These are all that are on my system, not specifically for this repo.

### Step 2: Prepare the Dataset

1. **Download** the TED-LIUM dataset from the link provided above.
2. **Place** the dataset contents into the project directory, specifically into `audio_files/` for audio files and `transcript_files/` for transcripts.

### Step 3: Run the Model

To execute the code, open the `vatt-rebuild-pytorch.ipynb` notebook. This notebook includes all the steps required to preprocess the data, build the model, and start training.

### Training Components

The following are the key components of the VATT model adaptation in this project:

1. **Audio and Text Tokenization**: Tokenizes long audio and text data into suitable embeddings for model processing.
2. **Positional Encoding**: Adds positional information to audio and text embeddings for sequence awareness.
3. **Transformer Encoder**: Separate modality-specific encoders for audio and text data.
4. **Multimodal Projection Head**: Projects audio and text embeddings into a common embedding space.
5. **Contrastive Loss with Noise Contrastive Estimation (NCE)**: Trains the model using contrastive learning to align audio and text embeddings in the common space.
6. **DropToken**: A technique for randomly dropping tokens to manage long-sequence data effectively.

### Training Loop

The model trains with a basic loop implementing gradient descent on the contrastive loss between paired audio and text embeddings. 

---

## Troubleshooting

If you encounter errors related to audio file processing, make sure all `.wav` files are correctly formatted. You can use tools like `ffmpeg` or `sox` to convert audio files to the correct format and sample rate if necessary.