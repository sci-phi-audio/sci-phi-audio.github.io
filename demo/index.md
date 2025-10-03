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
  .label { color: #0A2472; font-weight: 700; }   /* actual sound labels (green, bold) */
  .dir   { color: #991B1B; font-weight: 700; }   /* directions (red, bold) */
  .trans { color: #0A2472; font-style: italic; } /* transcript (green, italic) */

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


<!-- === 🎧 Real-RIR Sample 1 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 1</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_615_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">1000m^3</span>;<br>
        RT60=<span class="kv">0.2s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-50dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">bricks falling:</span>(<span class="kv">2.7s-4.5s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.4m</span>, <span class="kv">-22dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">dough hook tapping:</span>(<span class="kv">1.3s-2.6s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-25dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">coin sound effect:</span>(<span class="kv">7.9s-8.6s</span>, <span class="dir">horizontal back</span>, <span class="kv">2.0m</span>, <span class="kv">-30dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">However, no further action was taken by police.</span>’:<br>
        (<span class="kv">3.7s-7.8s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">27dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.2s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-72dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">toy train:</span>(<span class="kv">2.7s-4.4s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-21dB</span>, <span class="kv">28dB</span>);<br>
        <span class="label">wood block:</span>(<span class="kv">1.3s-2.1s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-22dB</span>, <span class="kv">21dB</span>);<br>
        <span class="label">bicycle bell:</span>(<span class="kv">7.9s-8.5s</span>, <span class="dir">horizontal back</span>, <span class="kv">0.8m</span>, <span class="kv">-26dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">However, no further action was taken by police.</span>’:<br>
        (<span class="kv">3.6s-7.3s</span>, <span class="dir">horizontal right</span>, <span class="kv">1.5m</span>, <span class="kv">-37dB</span>, <span class="kv">26dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 2 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 2</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_6810_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">700m^3</span>;<br>
        RT60=<span class="kv">0.2s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">not present</span>;<br>
        noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">guitar:</span>(<span class="kv">2.2s-4.6s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.0m</span>, <span class="kv">-27dB</span>, <span class="kv">25dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">Only one person can claim the credit.</span>’:<br>
        (<span class="kv">3.0s-6.1s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-33dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">shaker:</span>(<span class="kv">5.2s-7.2s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.0m</span>, <span class="kv">-35dB</span>, <span class="kv">25dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-80dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">piano:</span>(<span class="kv">2.2s-4.4s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-26dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">Only one person can claim the credit.</span>’:<br>
        (<span class="kv">2.9s-6.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-33dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">We deserved the three points.</span>’:<br>
        (<span class="kv">3.0s-6.8s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-38dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">shaker:</span>(<span class="kv">5.1s-7.2s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-38dB</span>, <span class="kv">24dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 3 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 3</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_7837_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">700m^3</span>;<br>
        RT60=<span class="kv">0.6s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient room noise</span>;<br>
        noise_loudness=<span class="kv">-64dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">Bongo, Congo:</span>(<span class="kv">1.9s-2.1s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-35dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">clapping:</span>(<span class="kv">1.6s-3.4s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-40dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">human speech:</span>(<span class="kv">5.8s-8.4s</span>, <span class="dir">lower back-right</span>, <span class="kv">1.5m</span>, <span class="kv">-46dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">ticking clock sound, voice:</span>(<span class="kv">4.5s-6.4s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-49dB</span>, <span class="kv">16dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">1.3s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-77dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">hit drum:</span>(<span class="kv">1.8s-2.2s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-36dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">hand clap:</span>(<span class="kv">1.7s-3.3s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.8m</span>, <span class="kv">-39dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">I am about protecting the state pension.</span>’:<br>
        (<span class="kv">5.1s-8.7s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">1.5m</span>, <span class="kv">-45dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">wood block:</span>(<span class="kv">4.6s-5.8s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-46dB</span>, <span class="kv">17dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 4 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 4</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_7995_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">700m^3</span>;<br>
        RT60=<span class="kv">0.3s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient environmental sounds</span>;<br>
        noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">female voice:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.1m</span>, <span class="kv">-28dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">Or maybe it's the other way around.</span>’:<br>
        (<span class="kv">3.9s-6.5s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">0.7m</span>, <span class="kv">-35dB</span>, <span class="kv">23dB</span>);<br>
        <span class="label">Military:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">upper front-right</span>, <span class="kv">1.4m</span>, <span class="kv">-38dB</span>, <span class="kv">18dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.5s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-62dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">Anyone remaining after that will be targeted.</span>’:<br>
        (<span class="kv">0.6s-5.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-26dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">Or maybe it's the other way around.</span>’:<br>
        (<span class="kv">3.4s-6.4s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.8m</span>, <span class="kv">-33dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">hand clap:</span>(<span class="kv">0.6s-2.3s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-34dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">toy train:</span>(<span class="kv">0.0s-4.5s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">1.5m</span>, <span class="kv">-34dB</span>, <span class="kv">14dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 5 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 5</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_8179_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">400m^3</span>;<br>
        RT60=<span class="kv">0.5s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-49dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">We don't want to be too intrusive.</span>’:<br>
        (<span class="kv">7.1s-9.8s</span>, <span class="dir">horizontal right</span>, <span class="kv">0.8m</span>, <span class="kv">-20dB</span>, <span class="kv">15dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">I guess they just can't help it.</span>’:<br>
        (<span class="kv">7.7s-10.0s</span>, <span class="dir">upper back-left</span>, <span class="kv">2.0m</span>, <span class="kv">-24dB</span>, <span class="kv">9dB</span>);<br>
        <span class="label">Congo drum:</span>(<span class="kv">6.5s-6.6s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.1m</span>, <span class="kv">-26dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">castanet:</span>(<span class="kv">0.4s-2.4s</span>, <span class="dir">horizontal back</span>, <span class="kv">1.8m</span>, <span class="kv">-38dB</span>, <span class="kv">9dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.7s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-65dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">We don't want to be too intrusive.</span>’:<br>
        (<span class="kv">7.1s-9.8s</span>, <span class="dir">horizontal right</span>, <span class="kv">0.8m</span>, <span class="kv">-20dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">That is my preference.</span>’:<br>
        (<span class="kv">7.7s-10.0s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.5m</span>, <span class="kv">-25dB</span>, <span class="kv">11dB</span>);<br>
        <span class="label">hit drum:</span>(<span class="kv">6.5s-6.8s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-26dB</span>, <span class="kv">11dB</span>);<br>
        <span class="label">wood block:</span>(<span class="kv">0.5s-1.9s</span>, <span class="dir">horizontal back</span>, <span class="kv">1.5m</span>, <span class="kv">-37dB</span>, <span class="kv">9dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 6 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 6</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_2429_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">2200m^3</span>;<br>
        RT60=<span class="kv">0.5s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">not present</span>;<br>
        noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">tapping of broom, concrete floor, wooden broom scrape, woody thump:</span>(<span class="kv">8.3s-9.2s</span>, <span class="dir">upper front-right</span>, <span class="kv">0.7m</span>, <span class="kv">-32dB</span>, <span class="kv">23dB</span>);<br>
        <span class="label">sax baritone:</span>(<span class="kv">3.5s-6.9s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.9m</span>, <span class="kv">-33dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">So, in a sense, it was a selfless act.</span>’:<br>
        (<span class="kv">0.0s-7.2s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">22dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.7s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-75dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">wood block:</span>(<span class="kv">8.3s-9.1s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">0.8m</span>, <span class="kv">-27dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">organ:</span>(<span class="kv">4.1s-5.9s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.5m</span>, <span class="kv">-30dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">So, in a sense, it was a government subsidy.</span>’:<br>
        (<span class="kv">3.1s-7.1s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-36dB</span>, <span class="kv">21dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 7 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 7</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_6735_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">1000m^3</span>;<br>
        RT60=<span class="kv">0.4s</span>;<br>
        n_src=<span class="kv">4</span>. noise_label: <span class="kv">thunder</span>;<br>
        noise_loudness=<span class="kv">-72dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">It's a delightful idea, but the implementation is extremely complicated.</span>’:<br>
        (<span class="kv">4.4s-7.3s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-42dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">Party is up for it!</span>’:<br>
        (<span class="kv">3.2s-5.5s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">0.7m</span>, <span class="kv">-43dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">That'll be the case on Tuesday.</span>’:<br>
        (<span class="kv">7.5s-9.7s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.3m</span>, <span class="kv">-50dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">footsteps on carpet:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">1.6m</span>, <span class="kv">-59dB</span>, <span class="kv">15dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.7s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-65dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">The party is up for it.</span>’:<br>
        (<span class="kv">2.9s-4.9s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-40dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">It's a delightful idea, but a distancing one.</span>’:<br>
        (<span class="kv">4.3s-7.7s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-41dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">That will be the case on Tuesday.</span>’:<br>
        (<span class="kv">7.5s-9.8s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.5m</span>, <span class="kv">-47dB</span>, <span class="kv">12dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 8 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 8</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_8538_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">500m^3</span>;<br>
        RT60=<span class="kv">0.4s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient background noise</span>;<br>
        noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">We want to sort it out.</span>’:<br>
        (<span class="kv">5.0s-7.3s</span>, <span class="dir">horizontal right</span>, <span class="kv">1.6m</span>, <span class="kv">-35dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">You need a trademark.</span>’:<br>
        (<span class="kv">7.4s-10.0s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-37dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">The man was obviously desperate enough to hire a private thief.</span>’:<br>
        (<span class="kv">0.2s-4.2s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.2m</span>, <span class="kv">-44dB</span>, <span class="kv">14dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-66dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">We want to sort it out.</span>’:<br>
        (<span class="kv">5.0s-7.3s</span>, <span class="dir">horizontal right</span>, <span class="kv">1.5m</span>, <span class="kv">-35dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">You need a trademark.</span>’:<br>
        (<span class="kv">7.4s-9.6s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">The man was obviously desperate to get away from the police.</span>’:<br>
        (<span class="kv">0.0s-4.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-42dB</span>, <span class="kv">12dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 9 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 9</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_9863_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">700m^3</span>;<br>
        RT60=<span class="kv">0.4s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient sounds</span>;<br>
        noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">brass bell:</span>(<span class="kv">2.4s-3.1s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-28dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">Military:</span>(<span class="kv">2.5s-8.6s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.1m</span>, <span class="kv">-30dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">percussion:</span>(<span class="kv">4.1s-6.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-40dB</span>, <span class="kv">19dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">1.7s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-85dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">bicycle bell:</span>(<span class="kv">2.4s-3.3s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.8m</span>, <span class="kv">-29dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">toy train:</span>(<span class="kv">3.1s-7.3s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-30dB</span>, <span class="kv">14dB</span>);<br>
        <span class="label">hand clap:</span>(<span class="kv">4.1s-5.6s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-38dB</span>, <span class="kv">15dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 10 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 10</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_1356_nsrc2.wav" type="audio/wav">
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
        room_volume=<span class="kv">500m^3</span>;<br>
        RT60=<span class="kv">0.4s</span>;<br>
        n_src=<span class="kv">1</span>. noise_label: <span class="kv">car horn</span>;<br>
        noise_loudness=<span class="kv">-35dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">That is giving me great confidence.</span>’:<br>
        (<span class="kv">2.8s-9.9s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-40dB</span>, <span class="kv">19dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;<br>
        n_src=<span class="kv">2</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-76dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">organ:</span>(<span class="kv">2.9s-5.0s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">1.5m</span>, <span class="kv">-22dB</span>, <span class="kv">11dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">That has given me great confidence.</span>’:<br>
        (<span class="kv">3.2s-6.1s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.8m</span>, <span class="kv">-36dB</span>, <span class="kv">17dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 11 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 11</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_5468_nsrc2.wav" type="audio/wav">
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
        room_volume=<span class="kv">1500m^3</span>;<br>
        RT60=<span class="kv">0.2s</span>;<br>
        n_src=<span class="kv">2</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">hi hat:</span>(<span class="kv">7.9s-9.9s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.8m</span>, <span class="kv">-28dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">They had to be cut from the wreckage.</span>’:<br>
        (<span class="kv">1.9s-6.2s</span>, <span class="dir">upper back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-39dB</span>, <span class="kv">28dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.2s</span>;<br>
        n_src=<span class="kv">2</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-72dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">shaker:</span>(<span class="kv">7.9s-10.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-29dB</span>, <span class="kv">25dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">They had to be cut from the wreckage.</span>’:<br>
        (<span class="kv">2.0s-6.2s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">30dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 12 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 12</b><br>
    <audio controls>
      <source src="../samples/real_rir/binaural/mix_5640_nsrc2.wav" type="audio/wav">
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
        room_volume=<span class="kv">1000m^3</span>;<br>
        RT60=<span class="kv">0.6s</span>;<br>
        n_src=<span class="kv">2</span>. noise_label: <span class="kv">ambient room sounds</span>;<br>
        noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">electronic alarm:</span>(<span class="kv">5.1s-9.7s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-34dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">That was never her agenda.</span>’:<br>
        (<span class="kv">0.1s-9.6s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-42dB</span>, <span class="kv">18dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.7s</span>;<br>
        n_src=<span class="kv">2</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-67dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">security buzzer:</span>(<span class="kv">6.1s-8.4s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">1.5m</span>, <span class="kv">-33dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">That was never their agenda.</span>’:<br>
        (<span class="kv">2.9s-5.8s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.5m</span>, <span class="kv">-42dB</span>, <span class="kv">17dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Real-RIR Sample 13 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Real-RIR Sample 13</b><br>
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
        room_volume=<span class="kv">200m^3</span>;<br>
        RT60=<span class="kv">0.5s</span>;<br>
        n_src=<span class="kv">3</span>. noise_label: <span class="kv">stairs</span>;<br>
        noise_loudness=<span class="kv">-79dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">He is an extraordinary writer on so many levels.</span>’:<br>
        (<span class="kv">5.0s-9.7s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.1m</span>, <span class="kv">-51dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">bell:</span>(<span class="kv">4.3s-9.8s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-53dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">Nature:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.1m</span>, <span class="kv">-64dB</span>, <span class="kv">10dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;<br>
        n_src=<span class="kv">2</span>. noise_label: <span class="kv">ambient noise</span>;<br>
        noise_loudness=<span class="kv">-74dB</span>.<br>
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


