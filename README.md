# Multimodal Film Copilot

An AI-assisted video player architecture designed to help advanced English learners (C1 level and above) fully understand the pronunciation, subtext, and cultural context of films and television series.

---

## Core Pain Points

At an advanced stage of language learning, traditional tools like dictionary lookups or full-sentence translations no longer solve the primary obstacles. Learners frequently encounter two main barriers:

1. **Fast Connected Speech (Listening Barriers):** Actors speak at rapid speeds, involving phonetic phenomena such as vowel reduction, elision, and flapping. Even when learners recognize every word in the subtitles, they often cannot distinguish the actual pronunciation in the audio track, even after multiple playbacks.
2. **Cultural Context and Subtext (Comprehension Barriers):** The literal meaning of a line may be simple, but the actor might use sarcasm, slang, local subcultures, or internet memes. Because text-only large language models cannot see the visual track, they provide rigid literal translations, leaving learners unable to understand the humor or true social intentions.

Most existing video learning extensions function essentially as advanced electronic dictionaries with minimal AI integration. Meanwhile, current AI media players only send subtitle text to the model, stripping away the necessary visual and acoustic context.

---

## Core Design: Synchronized Audio, Subtitles, and Screenshots

To address these pain points, this project designs a multimodal, real-time diagnostic pipeline.

When a user encounters connected speech or a cultural reference they do not understand and presses the pause button, the system automatically packages the three-dimensional modal data from the preceding time interval and sends it to a native multimodal large language model:

1. **Acoustic Stream:** Automatically extracts a 10–15 second audio slice from the track leading up to the pause.
2. **Text Stream:** Automatically extracts the subtitle text aligned with that specific time interval.
3. **Visual Stream:** Automatically captures several keyframe screenshots (the current paused frame and environmental interaction frames from a few seconds prior).

By simultaneously analyzing the audio, text, micro-expressions, and physical environment, the model performs a more accurate cross-modal analysis.

---

## Architecture and Dual-Engine Workflow

The first phase of the system uses a local execution path to minimize engineering complexity. It retrieves the playback progress of a local VLC media player via HTTP requests. When a hotkey is pressed, it calls local FFmpeg scripts to handle the audio slicing and image capturing.

Depending on the user's specific query, the system routes the data to one of two independent linguistic diagnostic engines:

### Engine 1: Phonetic and Speech Phenomenon Audit (For listening difficulties)
* **Inputs:** Audio + Subtitles + Screenshots.
* **Outputs:** 
  * An analysis of the acoustic reduction and elision mechanisms in the dialogue (explaining which sounds are omitted or linked).
  * A structured shadowing template highlighting stress anchors and dropped sounds.

### Engine 2: Context, Subtext, and Cultural Meme Audit (For comprehension difficulties)
* **Inputs:** Subtitles + Two Screenshots (providing physical environment, body language, and micro-expressions).
* **Outputs:** 
  * An explanation of the sarcasm, metaphors, or sociocultural background behind the dialogue.
  * An analysis comparing the literal meaning of the words against the speaker's actual social intent (subtext), integrated with the visual feedback of the listener in the scene.

---

## Project Status

This repository currently contains only the conceptual blueprint, system specification, and core multimodal prompts.

**Why is there no implementation code yet?**
The author is currently focusing their primary efforts on research projects within their university's Haptic Sensing Lab.

At a fundamental level, the logic of this media plugin (text + audio + vision = contextual grounding) shares the same core principles of multimodal sensor fusion as embodied AI (commands + haptics + vision = physical grounding). The author has decided to prioritize the study and accumulation of these technologies within the laboratory first.

This repository serves to publish the complete architectural design and its corresponding timestamp. Developers interested in the project are welcome to submit Pull Requests to implement the local VLC/FFmpeg integration scripts or open Issues to discuss architectural details.

---

## License

GNU General Public License v3.0 (GPL v3) - This project is open-sourced under the GPL v3 license. Any project modified or derived based on this code must remain open source and cannot be commercialized as closed-source software.
