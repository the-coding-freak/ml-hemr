# HEMR: Hypergraph Embeddings for Music Recommendation

## Overview

This project implements **HEMR (Hypergraph Embeddings for Music Recommendation)**, originally proposed in the paper:

> La Gatta, V., Moscato, V., Pennone, M., Postiglione, M., & Sperlí, G.
> *Music Recommendation via Hypergraph Embedding*. IEEE Transactions on Neural Networks and Learning Systems (TNNLS), 2023.

The goal of HEMR is to improve music recommendation quality by representing users, songs, artists, releases, and tags within a **hypergraph structure**, allowing higher-order relationships to be captured more effectively than traditional graph-based recommenders.

This repository contains:

* A complete dataset preprocessing pipeline
* Hypergraph construction following the paper methodology
* Random walk generation on hypergraphs
* Word2Vec-based embedding learning
* Recommendation generation using cosine similarity
* Additional optimizations for large-scale execution in Google Colab
* Mood-aware feature extensions (arousal and valence)

---

## Repository Structure

### `HEMR_preprocessing.ipynb`

Dataset preparation pipeline that transforms raw Million Song Dataset resources into the format required by HEMR.

Main tasks:

* Process Echo Nest Taste Profile data
* Extract user-song listening interactions
* Filter sparse users and invalid entries
* Extract song metadata
* Parse Last.fm tags
* Merge metadata sources
* Generate:

  * `user_data_final.csv`
  * `songs_final.csv`

### `HEMR_Colab_optimized_FULL_LITE.ipynb`

Main implementation of HEMR.

Pipeline stages:

1. Environment setup
2. Data loading and validation
3. Hypergraph construction
4. Random walk generation
5. Word2Vec embedding training
6. Recommendation generation
7. Evaluation and visualization
8. Mood-aware user profiling

---

## Methodology

The implementation follows the architecture proposed in the original HEMR paper.

### 1. Hypergraph Construction

The hypergraph contains five node types:

* Users
* Songs
* Artists
* Releases
* Tags

Four hyperedge categories are constructed:

* Listenings
* Albums
* Discographies
* Topics

This structure allows the model to capture complex many-to-many relationships that cannot be represented effectively in ordinary graphs.

---

### 2. Random Walk Generation

Hypergraph-aware random walks are generated following the traversal strategy described in the paper.

The walks:

* Explore neighborhood structure
* Capture contextual relationships
* Serve as training sequences for embedding generation

---

### 3. Embedding Learning

Node embeddings are learned using:

* Skip-Gram Word2Vec
* Context-window training
* Random-walk sequences as sentences

The resulting embeddings encode both:

* Structural relationships
* Contextual music information

---

### 4. Recommendation Generation

Recommendations are produced using cosine similarity between:

* User embeddings
* Song embeddings

Songs already present in a user's listening history are excluded from recommendation results.

---

### 5. Mood-Aware Extension

In addition to the original paper implementation, this project incorporates:

* Arousal scores
* Valence scores

These attributes are aggregated from song metadata and used to build user mood profiles for future recommendation enhancements.

---

## Dataset

The datasets are **not included** in this repository.

All data was obtained from publicly available external sources:

### Million Song Dataset (MSD)

Provides:

* Song metadata
* Artist information
* Release information

### Echo Nest Taste Profile Subset

Provides:

* User-song interactions
* Play counts

### Last.fm Dataset

Provides:

* User-generated tags
* Genre information
* Song descriptors

Users must independently download the datasets and place them in the locations specified in the preprocessing notebook.

---

## Generated Data Files

The preprocessing pipeline generates:

### User Data

`user_data_final.csv`

Columns:

* user
* song_id
* play_count

### Song Metadata

`songs_final.csv`

Columns include:

* song_id
* artist_name
* release
* title
* tags
* arousal
* valence
* lyrics_text

---

## Key Features

* Hypergraph-based recommendation framework
* Higher-order relationship modeling
* Hypergraph random walks
* Word2Vec embeddings
* Cosine similarity ranking
* Colab-optimized implementation
* Dataset preprocessing pipeline
* Visualization utilities
* Mood-aware extensions

---

## Running the Project

### Step 1 – Download Datasets

Obtain:

* Million Song Dataset
* Echo Nest Taste Profile Subset
* Last.fm Dataset

### Step 2 – Preprocess Data

Run:

`HEMR_preprocessing.ipynb`

Outputs:

* `user_data_final.csv`
* `songs_final.csv`

### Step 3 – Train HEMR

Run:

`HEMR_Colab_optimized_FULL_LITE.ipynb`

The notebook will:

* Build the hypergraph
* Generate random walks
* Train embeddings
* Produce recommendations
* Generate visualizations

---

## Results

The implementation reproduces the HEMR pipeline proposed in the paper and demonstrates the effectiveness of hypergraph embeddings for music recommendation. According to the original paper, HEMR achieves superior performance compared to several state-of-the-art recommendation baselines, particularly in top-K recommendation and cold-start scenarios.

---

## Acknowledgements

Original research:

La Gatta, V., Moscato, V., Pennone, M., Postiglione, M., & Sperlí, G.

*Music Recommendation via Hypergraph Embedding*, IEEE Transactions on Neural Networks and Learning Systems,2023.

This repository provides an implementation, preprocessing pipeline, and practical optimizations inspired by the published methodology.
