# LieLens – Context-Aware Deception Detection (HACK LLM)

LieLens is a contextual deception detection system designed for **Diplomacy-like multi-agent communication**, where players negotiate, make promises, and betray alliances.  
The system goes beyond surface-level text classification by **tracking commitments and checking their consistency over time**.

## Motivation

In strategy games like Diplomacy, deception is subtle and highly context-dependent.  
A message that appears honest in isolation can be deceptive when viewed against prior promises or agreements.

LieLens addresses this challenge by combining **semantic understanding of messages** with **explicit memory of commitments**, enabling reasoning about consistency across conversations.

## High-Level Approach

LieLens consists of the following components:

**Message Encoder**  
  DistilBERT encodes each message into a semantic representation.
**Commitment Memory**  
  Extracts and stores explicit promises (e.g., “I will not attack you”).
**Consistency Checker**  
  Compares new messages against stored commitments to detect contradictions.
**(Planned) Conversation Graph**  
  Models players as nodes and messages as directed edges to capture interaction context.
**Fusion Layer**  
  Combines message embeddings and commitment consistency signals.

This hybrid symbolic–neural design enables both **prediction** and **interpretability**.

## Dataset

We use the **Diplomacy dataset** provided in the hackathon.

Each sample includes:
- Message text
- Sender and receiver identifiers
- Deception label

The dataset presents challenges such as **label noise** and **class imbalance** between deceptive and truthful messages.

## Results

Performance was evaluated using class-weighted training to address imbalance.

**Observed performance:**
Accuracy: ~66–70%
Macro F1 score: ~0.40

While overall F1 remains modest due to dataset ambiguity, **commitment memory improved interpretability** by highlighting which prior promises contributed to deception predictions.

## Current Status

Implemented:
Transformer-based message encoder (DistilBERT)
Commitment memory and consistency checking
Manual PyTorch training loop

Planned:
Full Graph Attention Network for conversation modeling
Enhanced rationale extraction
Interactive demo deployment

## How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Train the model
python train.py

# Evaluate the model
python evaluate.py
