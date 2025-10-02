---
layout: review
---

<img src="../figures/model.png" style="width: 90%; display: block; margin: auto;">

<span style="color: black;">
<b>Abstract</b>: Acoustic scene perception spans what the sound is, when it occurs, where it is in direction and distance, and how it sounds in loudness and reverberation. While audio language models excel in sound recognition, single-channel input fundamentally limits spatial understanding. This work presents <em><strong>Sci-Phi</strong></em>, a spatial audio large language model with dual spatial and spectral encoders that estimates a complete parameter set for all sound sources and the surrounding environment. Learning from over 4,000 hours of synthetic first-order ambisonics recordings and their metadata, <em><strong>Sci-Phi</strong></em> enumerates and describes up to four sound sources in one pass, alongside background noise and room characteristics. We evaluate the model with a carefully designed permutation-invariant protocol and 15 metrics covering content, location, timing, loudness, and reverberation, and analyze its robustness across various signal-to-noise ratios, reverberation levels, and challenging cases such as spatially, temporally, or semantically overlapping sound sources. Notably, <em><strong>Sci-Phi</strong></em> generalizes to real room impulse responses with only minor performance degradation. Overall, this work establishes the first audio LLM capable of full spatial-scene description, with strong potential for real-world deployment.
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

<div style="background-color: #FFF2E5; padding: 15px; border-left: 5px solid #FFB899; font-style: italic;">
The audio samples were converted from ambisonics into binaural. We strongly recommend listening with a headset in order to hear spatial cues (source direction).
</div>

<hr style="height: 3px; background-color: grey; border: none;">


<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Audio Sample</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_575_nsrc2.wav" type="audio/wav">
      Your browser does not support the audio element.
    </audio>
  </div>
</div>

<div class="table-container">
  <table>
    <tr>
      <th>Generated Description</th>
      <th>Ground-truth Description</th>
    </tr>
    <tr>
      <td>room_volume=200m^3; RT60=0.5s; n_src=3.<br>
      noise_label:stairs; noise_loudness=-79dB.<br>
      Sound label:(time, direction, distance, loudness, C50):<br>
      English male speech with transcript 'He is an extraordinary writer on so many levels.':<br>
      (5.0s-9.7s,horizontal left,1.1m,-51dB,10dB);<br>
      bell:(4.3s-9.8s,horizontal front,0.8m,-53dB,12dB);<br>
      Nature:(0.0s-10.0s,horizontal left,1.1m,-64dB,10dB).<br>
</td>
      <td>room_volume=None; RT60=0.6s;<br>
      n_src=2. noise_label:ambient noise;noise_loudness=-74dB.<br>
      Sound label:(time, direction, distance, loudness, C50):<br>
      English male speech with transcript 'He is an extraordinary writer on so many levels.':<br>
      (4.9s-9.3s,horizontal left,1.5m,-49dB,9dB);<br>
      metallophone:(6.2s-9.0s,horizontal front,1.5m,-51dB,10dB).</td>
    </tr>
  </table>
</div>

<hr style="height: 3px; background-color: grey; border: none;">

UNDER CONSTRUCTION


