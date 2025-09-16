---
layout: arxiv
---

<img src="../figures/model.png" style="width: 70%; display: block; margin: auto;">

<span style="color: black;">
<b>Abstract</b>: Acoustic scene perception spans what the sound is, when it occurs, where it is in direction and distance, and how it sounds in loudness and reverberation. While audio language models excel in sound recognition, single-channel input fundamentally limits spatial understanding. This work presents \textit{Sci-Phi}, a spatial audio large language model with dual spatial and spectral encoders that estimates a complete parameter set for all sound sources and the surrounding environment. Learning from over 4,000 hours of synthetic first-order ambisonics recordings and their metadata, \textit{Sci-Phi} enumerates and describes up to four sound sources in one pass, alongside background noise and room characteristics. We evaluate the model with a carefully designed permutation-invariant protocol and 15 metrics covering content, location, timing, loudness, and reverberation, and analyze its robustness across various signal-to-noise ratios, reverberation levels, and challenging cases such as spatially, temporally, or semantically overlapping sound sources. Notably, \textit{Sci-Phi} generalizes to real room impulse responses with only minor performance degradation. Overall, this work establishes the first audio LLM capable of full spatial-scene description, with strong potential for real-world deployment.
</span>

<style>
  .table-container {
    overflow-x: auto;
    width: 100%;
  }
  table {
    width: max-content;
    border-collapse: collapse;
    border: 1px solid grey;
  }
  th, td {
    padding: 10px;
    border: 1px solid black;
    text-align: left;
    white-space: nowrap; /* Prevent text from wrapping */
  }
</style>

<style>
  .model-name {
    color: grey;
    font-weight: bold;
  }

  .model-name b {
    color: black;
  }
  
</style>

<hr style="height: 3px; background-color: grey; border: none;">



<hr style="height: 3px; background-color: grey; border: none;">


