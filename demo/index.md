---
layout: review
---

<img src="../figures/model.png" style="width: 90%; display: block; margin: auto;">


<style>
  /* Container + table layout */
  .table-container {
    overflow-x: auto;
    width: 100%;
    color: #6B7280;                 /* default gray text */
  }
  .table-container table {
    width: max-content;
    border-collapse: collapse;
    border: 1px solid grey;
  }
  .table-container th,
  .table-container td {
    padding: 10px;
    border: 1px solid black;
    text-align: left;
    vertical-align: top;            /* top-align cells */
  }

  /* Wrapping: headers stay on one line; cells wrap (or honor <br>) */
  .table-container th { white-space: nowrap; color:#111827; }
  .table-container td { white-space: normal; }   /* <= put this AFTER any th,td white-space rules */

  /* Coloring helpers */
  .kv    { color: #111827; font-weight: 700; }   /* numbers/units/values (black, bold) */
  .label { color: #065F46; font-weight: 700; }   /* actual sound labels (green, bold) */
  .dir   { color: #991B1B; font-weight: 700; }   /* directions (red, bold) */
  .trans { color: #065F46; font-style: italic; } /* transcript (green, italic) */

  /* Existing model-name styling */
  .model-name { color: grey; font-weight: bold; }
  .model-name b { color: black; }
</style>

<style>
  /* Container + table layout */
  .table-container {
    overflow-x: auto;
    width: 100%;
    color: #6B7280;                 /* default gray text */
  }
  .table-container table {
    width: max-content;
    border-collapse: collapse;
    border: 1px solid grey;
  }
  .table-container th,
  .table-container td {
    padding: 10px;
    border: 1px solid black;
    text-align: left;
    vertical-align: top;            /* top-align cells */
  }

  /* Wrapping: headers stay on one line; cells wrap (or honor <br>) */
  .table-container th { white-space: nowrap; color:#111827; }
  .table-container td { white-space: normal; }   /* <= put this AFTER any th,td white-space rules */

  /* Coloring helpers */
  .kv    { color: #111827; font-weight: 700; }   /* numbers/units/values (black, bold) */
  .label { color: #065F46; font-weight: 700; }   /* actual sound labels (green, bold) */
  .dir   { color: #991B1B; font-weight: 700; }   /* directions (red, bold) */
  .trans { color: #065F46; font-style: italic; } /* transcript (green, italic) */

  /* Existing model-name styling */
  .model-name { color: grey; font-weight: bold; }
  .model-name b { color: black; }
</style>


<span style="color: black;">
<b>Abstract</b>: Acoustic scene perception spans what the sound is, when it occurs, where it is in direction and distance, and how it sounds in loudness and reverberation. While audio language models excel in sound recognition, single-channel input fundamentally limits spatial understanding. This work presents <em><strong>Sci-Phi</strong></em>, a spatial audio large language model with dual spatial and spectral encoders that estimates a complete parameter set for all sound sources and the surrounding environment. Learning from over 4,000 hours of synthetic first-order ambisonics recordings and their metadata, <em><strong>Sci-Phi</strong></em> enumerates and describes up to four sound sources in one pass, alongside background noise and room characteristics. We evaluate the model with a carefully designed permutation-invariant protocol and 15 metrics covering content, location, timing, loudness, and reverberation, and analyze its robustness across various signal-to-noise ratios, reverberation levels, and challenging cases such as spatially, temporally, or semantically overlapping sound sources. Notably, <em><strong>Sci-Phi</strong></em> generalizes to real room impulse responses with only minor performance degradation. Overall, this work establishes the first audio LLM capable of full spatial-scene description, with strong potential for real-world deployment.
</span>

<div style="background-color: #FFF2E5; padding: 15px; border-left: 5px solid #FFB899; font-style: italic;">
The audio samples were converted from ambisonics into binaural for headphones. We strongly recommend wearing headphones to hear spatial cues (source direction).
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

<div class="table-container" markdown="0">
  <table>
    <tr>
      <th>Generated Description</th>
      <th>Ground-truth Description</th>
    </tr>
    <tr>
      <td>
        room_volume=<span class="kv">200m^3</span>; RT60=<span class="kv">0.5s</span>; n_src=<span class="kv">3</span>.<br>
        noise_label: <span class="kv">stairs</span>; noise_loudness=<span class="kv">-79dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">He is an extraordinary writer on so many levels.</span>’:<br>
        (<span class="kv">5.0s-9.7s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.1m</span>, <span class="kv">-51dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">bell:</span>(<span class="kv">4.3s-9.8s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-53dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">Nature:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.1m</span>, <span class="kv">-64dB</span>, <span class="kv">10dB</span>).<br>
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>; RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient noise</span>; noise_loudness=<span class="kv">-74dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">He is an extraordinary writer on so many levels.</span>’:<br>
        (<span class="kv">4.9s-9.3s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.5m</span>, <span class="kv">-49dB</span>, <span class="kv">9dB</span>);<br>
        <span class="label">metallophone:</span>(<span class="kv">6.2s-9.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-51dB</span>, <span class="kv">10dB</span>).
      </td>
    </tr>
  </table>
</div>


<hr style="height: 3px; background-color: grey; border: none;">

UNDER CONSTRUCTION


