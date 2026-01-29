# Synth Multisampler for OP-XY

Generate multisamples for OP-XY using 8 different synthesis engines for maximum sonic variety.

## Features

- **8 Synthesis Engines**:
  - **Modal Synthesis**: Vibrating structures, resonant modes
  - **Resonant**: Bandpass filters at harmonic frequencies for bell/vocal tones
  - **Sympathetic Strings**: Comb filters for sitar/harp-like resonance
  - **Plucked String**: Karplus-Strong algorithm
  - **Blown Pipe**: Waveguide physical model for flutes/brass
  - **2-Op FM**: Frequency modulation for metallic/bell tones
  - **Additive**: Pure harmonic synthesis for organ-like sounds
  - **Filtered Noise**: Bandpass filtered noise for wind/breath sounds

- **Universal Parameters** (meaning varies by engine):
  - **Structure**:
    - Modal: Harmonic spacing, inharmonicity
    - Resonant: Number of resonators (3-8), harmonic spacing
    - Sympathetic Strings: String detuning spread
    - Plucked String: Inharmonicity, string stiffness
    - FM: Modulation index (0-20)
    - Additive: Odd vs even harmonics
    - Noise: Number of bandpass filters
    - Waveguide: Breath noise amount
  - **Brightness**: High frequency content, filter cutoff, harmonic rolloff
  - **Damping**: Decay time, resonance, feedback amount
  - **Position**: Excitation location, formant spacing, phase offset

- **Modulation (LFO)**:
  - LFO Destination: Modulate Structure, Brightness, Damping, Position, or Pitch
  - LFO Waveform: Sine, Triangle, Square, or Random (Sample & Hold)
  - LFO Rate: 0.1 - 20 Hz
  - LFO Depth: Modulation intensity (0-100%)
  - Adds movement and organic character to sounds

- **Envelope & Excitation Controls**:
  - ADSR Envelope: Attack, Decay, Sustain, Release
  - Excitation Type: Impulse (strike), Noise burst, or Harmonic (pitched)
  - Excitation Intensity: Control the strength of the initial excitation

- **Smart Randomization**:
  - Pluck: Instant attack, bright, natural decay (guitar, bass, pizzicato)
  - Strings: Smooth attack, sustained, expressive (bowed, violin, cello)
  - Pad: Very slow attack, atmospheric, very long decay
  - Lead: Bright, articulate, fast attack, punchy
  - Bass: Dark, deep, fast attack, long sustain
  - SFX: Experimental, fully randomized all parameters

- **Export Format**:
  - OP-XY (.preset with individual WAVs + patch.json v4)
  - Automatic silence trimming (-60dB threshold)
  - 16-bit PCM WAV files optimized for OP-XY

- **Features**:
  - On-screen MIDI keyboard for previewing notes
  - Preview sounds before exporting
  - Configurable MIDI note range and increment
  - Smart key mapping with velocity layers

## Quick Start

### Local Development

```bash
# Start local server (from rings-multisampler directory)
npx http-server -p 8080

# Or use Python
python3 -m http.server 8080
```

Then open http://localhost:8080/rings.html in your browser.

## Engine Guide

### Best Uses for Each Engine

- **Modal**: Bells, metallic percussion, mallet instruments, pitched percussion
- **Resonant**: Bells, chimes, vocal formants, tuned resonators, crystal sounds
- **Sympathetic Strings**: Sitar, harp, tanpura, shimmering string resonance
- **Plucked String**: Guitar, bass, banjo, pizzicato strings
- **Blown Pipe**: Flute, recorder, pan pipes, brass, woodwinds
- **2-Op FM**: Electric pianos, bells, metallic leads, DX-style sounds
- **Additive**: Organs, drawbar sounds, pure tones, electronic pads
- **Filtered Noise**: Wind sounds, breath, ocean waves, air textures, vowels

### Usage

1. **Adjust Parameters**
   - Select synthesis engine from dropdown (8 engines organized by type)
   - Choose a sound type (Pluck, Strings, Pad, Lead, Bass, or SFX) and click "Randomize" for instant parameter generation
   - OR manually adjust structure, brightness, damping, position, envelope, and LFO controls
   - Use the on-screen keyboard to preview different notes
   - Click "Preview Sound" to hear middle C

2. **Configure Export**
   - Set preset name
   - Set key-on duration (default 3000ms)
   - Configure MIDI note range (default C2-C6 in semitone steps)

3. **Download**
   - Click "Download Multisample"
   - Generates .preset.zip ready to load into OP-XY
   - Includes trimmed 16-bit WAV files + patch.json

## Technical Details

### Synthesis Engines

**Physical Models:**
- **Modal Synthesis**: 8 resonant modes with exponential decay, configurable harmonic spacing
- **Resonant**: 3-8 bandpass filters at harmonic frequencies with formant-like positioning
- **Sympathetic Strings**: 5 detuned comb filters with averaging filter and feedback control
- **Plucked String**: Karplus-Strong with delay line, filtering, and inharmonicity
- **Blown Pipe**: Waveguide with breath noise and reflection coefficients

**Spectral:**
- **2-Op FM**: Classic frequency modulation with time-varying modulation index
- **Additive**: 16 harmonics with individual control over amplitude and phase
- **Filtered Noise**: White noise through multiple bandpass filters (1-5 formants)

### Output Specifications

- Sample Rate: AudioContext sample rate (typically 44.1kHz or 48kHz)
- Bit Depth: 32-bit float (internal synthesis) → 16-bit PCM (export)
- Format: Mono WAV files
- Silence trimming: -60dB threshold
- OP-XY patch.json format: v4 with regions, key mapping, loop points

## Credits

- Modal synthesis inspired by [Mutable Instruments Rings](https://github.com/pichenettes/eurorack) (Emilie Gillet)
- Synthesis engine implementations by Chad Furrow
- Export code adapted from [tv7-js DX7 tool](https://github.com/cfurrow7/tv7-multisampler)

## License

MIT License

## Links

- [Mutable Instruments Rings Documentation](https://pichenettes.github.io/mutable-instruments-documentation/modules/rings/)
- [Mutable Instruments Eurorack Source Code](https://github.com/pichenettes/eurorack)
- [DX7 Multisampler Tool](https://github.com/cfurrow7/tv7-multisampler)
