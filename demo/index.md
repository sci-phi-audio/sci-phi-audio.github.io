---
layout: review
---

<u>***Xilin Jiang***</u> (Columbia University, work done as an intern in MSR), <u>***Hannes Gamper***</u> (Microsoft Research), <u>***Sebastian Braun***</u> (Microsoft Research)

<img src="../figures/model.png" style="width: 90%; display: block; margin: auto;">

<style>
  /* Accordion */
  details.accordion { border: 1px solid #E5E7EB; border-radius: .5rem; margin: 1rem 0; background:#FFFFFF; }
  details.accordion > summary {
    list-style: none; cursor: pointer; padding: .75rem 1rem; font-weight: 700; color:#111827;
    display:flex; align-items:center; justify-content:space-between; gap:.75rem;
  }
  details.accordion[open] > summary { border-bottom: 1px solid #E5E7EB; }
  details.accordion .section-body { padding: 1rem; }
  /* Chevron */
  .chev { transition: transform .2s ease; }
  details[open] .chev { transform: rotate(90deg); }
  /* Optional toolbar */
  .accordion-toolbar {
    display:flex; gap:.5rem; justify-content:flex-end; margin: .5rem 0 1rem;
  }
  .accordion-btn {
    font: inherit; padding:.4rem .6rem; border:1px solid #D1D5DB; border-radius:.375rem; background:#F9FAFB; cursor:pointer;
  }
  .accordion-btn:hover { background:#F3F4F6; }
</style>
<script>
  function setAllAccordions(open) {
    document.querySelectorAll('details.accordion').forEach(d => d.open = open);
  }
</script>

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

<script>
document.addEventListener('click', function (e) {
  const btn = e.target.closest('.gt-toggle');
  if (!btn) return;

  const targetId = btn.getAttribute('data-target');
  const table = document.getElementById(targetId);
  if (!table) return;

  const expanded = btn.getAttribute('aria-expanded') === 'true';
  const gtRows = table.querySelectorAll('.gt-row');

  gtRows.forEach(row => row.style.display = expanded ? 'none' : 'table-row');
  btn.setAttribute('aria-expanded', (!expanded).toString());
  btn.textContent = expanded ? 'Show the ground-truth' : 'Hide the ground-truth';
});
</script>

<style>
  .gt-header {
    display: flex; align-items: center; justify-content: space-between; gap: .75rem;
  }
  .gt-toggle {
    font: inherit; padding: .25rem .5rem; border: 1px solid #D1D5DB; border-radius: .375rem;
    background: #F9FAFB; cursor: pointer;
  }
  .gt-toggle:hover { background: #F3F4F6; }
  /* Make the Ground-truth section visually distinct when shown */
  .gt-heading {
    background: #F9FAFB; color: #111827; font-weight: 600;
  }
</style>

<span style="color: black;">
<b>Abstract</b>: Acoustic scene perception spans what the sound is, when it occurs, where it is in direction and distance, and how it sounds in loudness and reverberation. While audio language models excel in sound recognition, single-channel input fundamentally limits spatial understanding. This work presents <em><strong>Sci-Phi</strong></em>, a spatial audio large language model with dual spatial and spectral encoders that estimates a complete parameter set for all sound sources and the surrounding environment. Learning from over 4,000 hours of synthetic first-order ambisonics recordings and their metadata, <em><strong>Sci-Phi</strong></em> enumerates and describes up to four sound sources in one pass, alongside background noise and room characteristics. We evaluate the model with a carefully designed permutation-invariant protocol and 15 metrics covering content, location, timing, loudness, and reverberation, and analyze its robustness across various signal-to-noise ratios, reverberation levels, and challenging cases such as spatially, temporally, or semantically overlapping sound sources. Notably, <em><strong>Sci-Phi</strong></em> generalizes to real room impulse responses with only minor performance degradation. Overall, this work establishes the first audio LLM capable of full spatial-scene description, with strong potential for real-world deployment.
</span>

<div style="background-color: #FFF2E5; padding: 15px; border-left: 5px solid #FFB899; font-style: italic;">
The audio samples were converted from ambisonics into binaural for headphones. We strongly recommend wearing headphones to hear spatial cues (source direction).
</div>

<hr style="height: 3px; background-color: grey; border: none;">

<!-- ========== Real-RIR (END) ========== -->

<!-- ========== Synthetic-RIR (START) ========== -->
<details class="accordion">
  <summary>Synthetic-RIR Samples<span class="chev">▶</span></summary>
  <div class="section-body">
<!-- === 🎧 Synthetic-RIR Sample 1 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 1</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_8729_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">1000m^3</span>;
        RT60=<span class="kv">0.4s</span>;
        n_src=<span class="kv">4</span>. <br>noise_label: <span class="kv">ambient sound</span>;
        noise_loudness=<span class="kv">-45dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">I can understand why they have gone away.</span>’:<br>
        (<span class="kv">5.3s-8.2s</span>, <span class="dir">upper front-left</span>, <span class="kv">0.8m</span>, <span class="kv">-18dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">Nature:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">3.0m</span>, <span class="kv">-25dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">fingers on teeth:</span>(<span class="kv">8.0s-8.1s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.2m</span>, <span class="kv">-28dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">kick bass drum:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">3.4m</span>, <span class="kv">-33dB</span>, <span class="kv">12dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">1900m^3</span>;
        RT60=<span class="kv">0.4s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient electronic hum</span>;noise_loudness=<span class="kv">-48dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">I can understand why they have gone.</span>’:<br>
        (<span class="kv">5.2s-8.5s</span>, <span class="dir">upper front-left</span>, <span class="kv">1.3m</span>, <span class="kv">-19dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">Bonapartes Gull:</span>(<span class="kv">0.1s-8.5s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">4.4m</span>, <span class="kv">-25dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">baseball bat swing:</span>(<span class="kv">7.8s-8.5s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.6m</span>, <span class="kv">-28dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">axe chopping:</span>(<span class="kv">0.0s-7.5s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">4.4m</span>, <span class="kv">-35dB</span>, <span class="kv">11dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 2 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 2</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_6715_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">1500m^3</span>;
        RT60=<span class="kv">0.3s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient sounds</span>;noise_loudness=<span class="kv">-59dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">Of course, on a diet like this one, I wouldn't recommend.</span>’:<br>
        (<span class="kv">4.1s-8.2s</span>, <span class="dir">upper front-left</span>, <span class="kv">0.8m</span>, <span class="kv">-33dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">That goes without saying.</span>’:<br>
        (<span class="kv">4.1s-6.4s</span>, <span class="dir">lower back-right</span>, <span class="kv">1.6m</span>, <span class="kv">-33dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">Nature:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">2.0m</span>, <span class="kv">-42dB</span>, <span class="kv">20dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">1900m^3</span>;
        RT60=<span class="kv">0.3s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">computer powering down</span>;noise_loudness=<span class="kv">-58dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">Of course, on Tuesday, United were beaten despite this.</span>’:<br>
        (<span class="kv">4.0s-7.9s</span>, <span class="dir">upper front-left</span>, <span class="kv">0.8m</span>, <span class="kv">-33dB</span>, <span class="kv">24dB</span>);<br>
        <span class="label">censor beep:</span>(<span class="kv">4.7s-5.4s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">2.0m</span>, <span class="kv">-36dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">That doesn't happen in Europe.</span>’:<br>
        (<span class="kv">3.6s-6.2s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">2.3m</span>, <span class="kv">-36dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">rattlesnake rattle:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">2.9m</span>, <span class="kv">-42dB</span>, <span class="kv">14dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 3 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 3</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_2280_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">200m^3</span>;
        RT60=<span class="kv">0.5s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">rain</span>;noise_loudness=<span class="kv">-47dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">female voice:</span>(<span class="kv">4.7s-6.6s</span>, <span class="dir">lower front-right</span>, <span class="kv">1.1m</span>, <span class="kv">-25dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">applause:</span>(<span class="kv">2.0s-7.8s</span>, <span class="dir">lower back-right</span>, <span class="kv">2.4m</span>, <span class="kv">-26dB</span>, <span class="kv">7dB</span>);<br>
        <span class="label">kettle pouring:</span>(<span class="kv">1.2s-9.4s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">0.8m</span>, <span class="kv">-34dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">The briefcase held the day's knives.</span>’:<br>
        (<span class="kv">1.8s-4.7s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.0m</span>, <span class="kv">-37dB</span>, <span class="kv">11dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">200m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">storm</span>;noise_loudness=<span class="kv">-49dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">You must be ready to play anyone.</span>’:<br>
        (<span class="kv">3.8s-6.8s</span>, <span class="dir">lower front-right</span>, <span class="kv">0.8m</span>, <span class="kv">-26dB</span>, <span class="kv">11dB</span>);<br>
        <span class="label">audience applause:</span>(<span class="kv">1.7s-8.3s</span>, <span class="dir">lower back-right</span>, <span class="kv">2.2m</span>, <span class="kv">-27dB</span>, <span class="kv">6dB</span>);<br>
        <span class="label">hot water pouring:</span>(<span class="kv">1.1s-8.9s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">0.8m</span>, <span class="kv">-36dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">Everyone is taking a breath and waiting.</span>’:<br>
        (<span class="kv">1.5s-5.4s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">1.4m</span>, <span class="kv">-37dB</span>, <span class="kv">8dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 4 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 4</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_2952_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">800m^3</span>;
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">rain</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">animal growling:</span>(<span class="kv">2.6s-6.9s</span>, <span class="dir">upper front</span>, <span class="kv">0.8m</span>, <span class="kv">-15dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">dog barking, dog growling, dog whimpering:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal left</span>, <span class="kv">2.4m</span>, <span class="kv">-26dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">robotic voice:</span>(<span class="kv">0.6s-4.2s</span>, <span class="dir">horizontal front</span>, <span class="kv">5.5m</span>, <span class="kv">-28dB</span>, <span class="kv">6dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">I should think so too.</span>’:<br>
        (<span class="kv">4.5s-6.8s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">2.4m</span>, <span class="kv">-32dB</span>, <span class="kv">9dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">600m^3</span>;
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">thunder</span>;noise_loudness=<span class="kv">-54dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">zombie, demon:</span>(<span class="kv">2.8s-6.0s</span>, <span class="dir">upper front</span>, <span class="kv">0.7m</span>, <span class="kv">-13dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">doberman pincher, barking:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.9m</span>, <span class="kv">-25dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">woosh, slow motion effect:</span>(<span class="kv">0.5s-4.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">6.1m</span>, <span class="kv">-26dB</span>, <span class="kv">6dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">I should think so, too.</span>’:<br>
        (<span class="kv">4.6s-6.8s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">2.5m</span>, <span class="kv">-32dB</span>, <span class="kv">9dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 5 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 5</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_5438_nsrc4.wav" type="audio/wav">
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
        room_volume=<span class="kv">400m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">environmental sounds</span>;noise_loudness=<span class="kv">-52dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">soda can opening:</span>(<span class="kv">3.6s-4.3s</span>, <span class="dir">horizontal right</span>, <span class="kv">0.8m</span>, <span class="kv">-27dB</span>, <span class="kv">15dB</span>);<br>
        <span class="label">ringtone:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">upper front-left</span>, <span class="kv">0.8m</span>, <span class="kv">-29dB</span>, <span class="kv">15dB</span>);<br>
        <span class="label">Nature:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">15dB</span>);<br>
        <span class="label">French speech</span> with transcript ‘<span class="trans">Il est le père de František Kaberle et Tomáš Kaberle.</span>’:<br>
        (<span class="kv">3.7s-8.4s</span>, <span class="dir">lower back-left</span>, <span class="kv">2.1m</span>, <span class="kv">-42dB</span>, <span class="kv">9dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">700m^3</span>;
        RT60=<span class="kv">0.5s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">bell</span>;noise_loudness=<span class="kv">-54dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">beer can opening:</span>(<span class="kv">3.6s-5.7s</span>, <span class="dir">horizontal right</span>, <span class="kv">1.4m</span>, <span class="kv">-29dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">phone ringing:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">upper front-left</span>, <span class="kv">1.3m</span>, <span class="kv">-30dB</span>, <span class="kv">14dB</span>);<br>
        <span class="label">bear growling, bear roaring:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">1.2m</span>, <span class="kv">-39dB</span>, <span class="kv">14dB</span>);<br>
        <span class="label">voice, dice rolling:</span>(<span class="kv">4.6s-9.6s</span>, <span class="dir">lower back</span>, <span class="kv">3.4m</span>, <span class="kv">-42dB</span>, <span class="kv">8dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 6 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 6</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_4550_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">1500m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">I've lost my head.</span>’:<br>
        (<span class="kv">2.2s-5.6s</span>, <span class="dir">horizontal back</span>, <span class="kv">2.6m</span>, <span class="kv">-38dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">A final agreement has not yet been completed.</span>’:<br>
        (<span class="kv">1.2s-4.6s</span>, <span class="dir">upper left</span>, <span class="kv">1.0m</span>, <span class="kv">-41dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">There was no time to mark.</span>’:<br>
        (<span class="kv">6.2s-8.2s</span>, <span class="dir">lower right</span>, <span class="kv">2.8m</span>, <span class="kv">-41dB</span>, <span class="kv">13dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">1000m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">I lost my head.</span>’:<br>
        (<span class="kv">3.1s-5.6s</span>, <span class="dir">horizontal back</span>, <span class="kv">2.6m</span>, <span class="kv">-38dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">A final agreement has not yet been completed.</span>’:<br>
        (<span class="kv">1.3s-4.4s</span>, <span class="dir">upper left</span>, <span class="kv">0.9m</span>, <span class="kv">-40dB</span>, <span class="kv">19dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">There was no time scale.</span>’:<br>
        (<span class="kv">6.2s-8.4s</span>, <span class="dir">lower right</span>, <span class="kv">2.5m</span>, <span class="kv">-42dB</span>, <span class="kv">12dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 7 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 7</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_1076_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">500m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient bathroom sounds</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">aluminium foil tearing:</span>(<span class="kv">6.3s-6.8s</span>, <span class="dir">horizontal back</span>, <span class="kv">1.2m</span>, <span class="kv">-25dB</span>, <span class="kv">14dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">We were in different places, and we talked for a while.</span>’:<br>
        (<span class="kv">0.5s-4.1s</span>, <span class="dir">lower back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-28dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">fart:</span>(<span class="kv">8.6s-9.9s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">2.4m</span>, <span class="kv">-43dB</span>, <span class="kv">10dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">500m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">horn</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">patting or tapping:</span>(<span class="kv">6.3s-6.6s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">1.6m</span>, <span class="kv">-26dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">We were in different places, usually in cellars.</span>’:<br>
        (<span class="kv">0.5s-4.6s</span>, <span class="dir">lower back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-28dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">fart:</span>(<span class="kv">8.6s-10.0s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">2.7m</span>, <span class="kv">-44dB</span>, <span class="kv">10dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 8 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 8</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_1144_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">500m^3</span>;
        RT60=<span class="kv">0.8s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">fireworks</span>;noise_loudness=<span class="kv">-68dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">explosion-like sound:</span>(<span class="kv">5.7s-9.1s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.1m</span>, <span class="kv">-45dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">water pouring:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">upper front</span>, <span class="kv">1.4m</span>, <span class="kv">-48dB</span>, <span class="kv">9dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">I always fall asleep when I'm doing something.</span>’:<br>
        (<span class="kv">5.2s-8.6s</span>, <span class="dir">lower right</span>, <span class="kv">1.1m</span>, <span class="kv">-48dB</span>, <span class="kv">10dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">900m^3</span>;
        RT60=<span class="kv">0.9s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">priest walking in hard sole shoes</span>;noise_loudness=<span class="kv">-66dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">time bomb:</span>(<span class="kv">1.8s-8.3s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.6m</span>, <span class="kv">-47dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">pouring drink:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">upper front</span>, <span class="kv">2.1m</span>, <span class="kv">-48dB</span>, <span class="kv">9dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">I always felt that I was in control of the match.</span>’:<br>
        (<span class="kv">5.3s-8.9s</span>, <span class="dir">lower front-right</span>, <span class="kv">2.1m</span>, <span class="kv">-48dB</span>, <span class="kv">9dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 9 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 9</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_1339_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">1300m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">button click:</span>(<span class="kv">1.9s-2.4s</span>, <span class="dir">horizontal right</span>, <span class="kv">7.0m</span>, <span class="kv">-32dB</span>, <span class="kv">6dB</span>);<br>
        <span class="label">coin drop:</span>(<span class="kv">7.7s-8.5s</span>, <span class="dir">upper back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-35dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">metal band:</span>(<span class="kv">1.5s-3.4s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">2.5m</span>, <span class="kv">-42dB</span>, <span class="kv">10dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">1000m^3</span>;
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">button click:</span>(<span class="kv">1.9s-6.9s</span>, <span class="dir">horizontal right</span>, <span class="kv">9.5m</span>, <span class="kv">-34dB</span>, <span class="kv">6dB</span>);<br>
        <span class="label">metal impact:</span>(<span class="kv">7.8s-8.5s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.7m</span>, <span class="kv">-35dB</span>, <span class="kv">18dB</span>);<br>
        <span class="label">boxing bell:</span>(<span class="kv">1.6s-3.3s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">2.6m</span>, <span class="kv">-41dB</span>, <span class="kv">9dB</span>).
      </td>
    </tr>
  </table>
</div>

<!-- === 🎧 Synthetic-RIR Sample 10 === -->
<div style="display: flex; align-items: center; gap: 20px;">
  <div>
    <b>🎧 Synthetic-RIR Sample 10</b><br>
    <audio controls>
      <source src="../samples/synthetic_rir/binaural/mix_1358_nsrc3.wav" type="audio/wav">
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
        room_volume=<span class="kv">500m^3</span>;
        RT60=<span class="kv">0.8s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">human scream:</span>(<span class="kv">0.1s-7.1s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">1.1m</span>, <span class="kv">-31dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">drum, snare:</span>(<span class="kv">1.8s-2.0s</span>, <span class="dir">upper back-right</span>, <span class="kv">0.9m</span>, <span class="kv">-42dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">A thousand years ago, the city was the center of an ancient civilisation.</span>’:<br>
        (<span class="kv">4.7s-8.9s</span>, <span class="dir">lower back-left</span>, <span class="kv">1.8m</span>, <span class="kv">-44dB</span>, <span class="kv">9dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">600m^3</span>;
        RT60=<span class="kv">0.8s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">crow:</span>(<span class="kv">0.4s-6.4s</span>, <span class="dir">horizontal front-right</span>, <span class="kv">1.2m</span>, <span class="kv">-31dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">punch:</span>(<span class="kv">1.8s-2.2s</span>, <span class="dir">upper back-right</span>, <span class="kv">1.1m</span>, <span class="kv">-42dB</span>, <span class="kv">13dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">A thousand years ago the church was a powerful force in Europe.</span>’:<br>
        (<span class="kv">4.6s-8.8s</span>, <span class="dir">lower back-left</span>, <span class="kv">2.3m</span>, <span class="kv">-44dB</span>, <span class="kv">9dB</span>).
      </td>
    </tr>
  </table>
</div>

  </div>
</details>
<!-- ========== Synthetic-RIR (END) ========== -->




<!-- ========== Real-RIR (START) ========== -->
<details class="accordion">
  <summary>Real-RIR Samples<span class="chev">▶</span></summary>
  <div class="section-body">
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
        room_volume=<span class="kv">1000m^3</span>;
        RT60=<span class="kv">0.2s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-50dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">bricks falling:</span>(<span class="kv">2.7s-4.5s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.4m</span>, <span class="kv">-22dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">dough hook tapping:</span>(<span class="kv">1.3s-2.6s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-25dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">coin sound effect:</span>(<span class="kv">7.9s-8.6s</span>, <span class="dir">horizontal back</span>, <span class="kv">2.0m</span>, <span class="kv">-30dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">However, no further action was taken by police.</span>’:<br>
        (<span class="kv">3.7s-7.8s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">27dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.2s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-72dB</span>.<br>
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
        room_volume=<span class="kv">700m^3</span>;
        RT60=<span class="kv">0.2s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">guitar:</span>(<span class="kv">2.2s-4.6s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.0m</span>, <span class="kv">-27dB</span>, <span class="kv">25dB</span>);<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">Only one person can claim the credit.</span>’:<br>
        (<span class="kv">3.0s-6.1s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-33dB</span>, <span class="kv">27dB</span>);<br>
        <span class="label">shaker:</span>(<span class="kv">5.2s-7.2s</span>, <span class="dir">horizontal back-left</span>, <span class="kv">1.0m</span>, <span class="kv">-35dB</span>, <span class="kv">25dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-80dB</span>.<br>
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
        room_volume=<span class="kv">700m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient room noise</span>;noise_loudness=<span class="kv">-64dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">Bongo, Congo:</span>(<span class="kv">1.9s-2.1s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-35dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">clapping:</span>(<span class="kv">1.6s-3.4s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-40dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">human speech:</span>(<span class="kv">5.8s-8.4s</span>, <span class="dir">lower back-right</span>, <span class="kv">1.5m</span>, <span class="kv">-46dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">ticking clock sound, voice:</span>(<span class="kv">4.5s-6.4s</span>, <span class="dir">horizontal back-right</span>, <span class="kv">0.8m</span>, <span class="kv">-49dB</span>, <span class="kv">16dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">1.3s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-77dB</span>.<br>
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
        room_volume=<span class="kv">700m^3</span>;
        RT60=<span class="kv">0.3s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient environmental sounds</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">female voice:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.1m</span>, <span class="kv">-28dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">Or maybe it's the other way around.</span>’:<br>
        (<span class="kv">3.9s-6.5s</span>, <span class="dir">horizontal front-left</span>, <span class="kv">0.7m</span>, <span class="kv">-35dB</span>, <span class="kv">23dB</span>);<br>
        <span class="label">Military:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">upper front-right</span>, <span class="kv">1.4m</span>, <span class="kv">-38dB</span>, <span class="kv">18dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.5s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-62dB</span>.<br>
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
        room_volume=<span class="kv">400m^3</span>;
        RT60=<span class="kv">0.5s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-49dB</span>.<br>
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
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-65dB</span>.<br>
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
        room_volume=<span class="kv">2200m^3</span>;
        RT60=<span class="kv">0.5s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">not present</span>;noise_loudness=<span class="kv">None</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">tapping of broom, concrete floor, wooden broom scrape, woody thump:</span>(<span class="kv">8.3s-9.2s</span>, <span class="dir">upper front-right</span>, <span class="kv">0.7m</span>, <span class="kv">-32dB</span>, <span class="kv">23dB</span>);<br>
        <span class="label">sax baritone:</span>(<span class="kv">3.5s-6.9s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.9m</span>, <span class="kv">-33dB</span>, <span class="kv">16dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">So, in a sense, it was a selfless act.</span>’:<br>
        (<span class="kv">0.0s-7.2s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-37dB</span>, <span class="kv">22dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-75dB</span>.<br>
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
        room_volume=<span class="kv">1000m^3</span>;
        RT60=<span class="kv">0.4s</span>;
        n_src=<span class="kv">4</span>.<br>noise_label: <span class="kv">thunder</span>;noise_loudness=<span class="kv">-72dB</span>.<br>
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
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-65dB</span>.<br>
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
        room_volume=<span class="kv">500m^3</span>;
        RT60=<span class="kv">0.4s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient background noise</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
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
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-66dB</span>.<br>
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
        room_volume=<span class="kv">700m^3</span>;
        RT60=<span class="kv">0.4s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient sounds</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">brass bell:</span>(<span class="kv">2.4s-3.1s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-28dB</span>, <span class="kv">20dB</span>);<br>
        <span class="label">Military:</span>(<span class="kv">2.5s-8.6s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.1m</span>, <span class="kv">-30dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">percussion:</span>(<span class="kv">4.1s-6.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-40dB</span>, <span class="kv">19dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">1.7s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-85dB</span>.<br>
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
        room_volume=<span class="kv">500m^3</span>;
        RT60=<span class="kv">0.4s</span>;
        n_src=<span class="kv">1</span>.<br>noise_label: <span class="kv">car horn</span>;noise_loudness=<span class="kv">-35dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">That is giving me great confidence.</span>’:<br>
        (<span class="kv">2.8s-9.9s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-40dB</span>, <span class="kv">19dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-76dB</span>.<br>
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
        room_volume=<span class="kv">1500m^3</span>;
        RT60=<span class="kv">0.2s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">hi hat:</span>(<span class="kv">7.9s-9.9s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.8m</span>, <span class="kv">-28dB</span>, <span class="kv">22dB</span>);<br>
        <span class="label">English female speech</span> with transcript ‘<span class="trans">They had to be cut from the wreckage.</span>’:<br>
        (<span class="kv">1.9s-6.2s</span>, <span class="dir">upper back-left</span>, <span class="kv">0.8m</span>, <span class="kv">-39dB</span>, <span class="kv">28dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.2s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-72dB</span>.<br>
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
        room_volume=<span class="kv">1000m^3</span>;
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient room sounds</span>;noise_loudness=<span class="kv">-55dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">electronic alarm:</span>(<span class="kv">5.1s-9.7s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-34dB</span>, <span class="kv">17dB</span>);<br>
        <span class="label">English speech</span> with transcript ‘<span class="trans">That was never her agenda.</span>’:<br>
        (<span class="kv">0.1s-9.6s</span>, <span class="dir">horizontal left</span>, <span class="kv">0.7m</span>, <span class="kv">-42dB</span>, <span class="kv">18dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.7s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-67dB</span>.<br>
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
        room_volume=<span class="kv">200m^3</span>;
        RT60=<span class="kv">0.5s</span>;
        n_src=<span class="kv">3</span>.<br>noise_label: <span class="kv">stairs</span>;noise_loudness=<span class="kv">-79dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">He is an extraordinary writer on so many levels.</span>’:<br>
        (<span class="kv">5.0s-9.7s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.1m</span>, <span class="kv">-51dB</span>, <span class="kv">10dB</span>);<br>
        <span class="label">bell:</span>(<span class="kv">4.3s-9.8s</span>, <span class="dir">horizontal front</span>, <span class="kv">0.8m</span>, <span class="kv">-53dB</span>, <span class="kv">12dB</span>);<br>
        <span class="label">Nature:</span>(<span class="kv">0.0s-10.0s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.1m</span>, <span class="kv">-64dB</span>, <span class="kv">10dB</span>).
      </td>
      <td>
        room_volume=<span class="kv">Unknown</span>;<br>
        RT60=<span class="kv">0.6s</span>;
        n_src=<span class="kv">2</span>.<br>noise_label: <span class="kv">ambient noise</span>;noise_loudness=<span class="kv">-74dB</span>.<br>
        Sound label: (time, direction, distance, loudness, C50):<br>
        <span class="label">English male speech</span> with transcript ‘<span class="trans">He is an extraordinary writer on so many levels.</span>’:<br>
        (<span class="kv">4.9s-9.3s</span>, <span class="dir">horizontal left</span>, <span class="kv">1.5m</span>, <span class="kv">-49dB</span>, <span class="kv">9dB</span>);<br>
        <span class="label">metallophone:</span>(<span class="kv">6.2s-9.0s</span>, <span class="dir">horizontal front</span>, <span class="kv">1.5m</span>, <span class="kv">-51dB</span>, <span class="kv">10dB</span>).
      </td>
    </tr>
  </table>
</div>


  </div>
</details>
