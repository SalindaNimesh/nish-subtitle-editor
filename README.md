# NISH — Google API subtitle editor MVP

A beginner-friendly dark subtitle editing app inspired by modern subtitle workspaces.

## Features included
- Local video preview and upload
- Import/edit subtitle cues and timings
- Add/delete subtitle lines; click cues to seek
- Subtitle font size, colour, bold and outline controls
- Animated subtitle preview presets: Pop In, Soft Fade, Bounce, Typewriter, Neon Glow, Slide Up, Karaoke Highlight and None
- SRT and VTT export
- Optional Google Gemini API transcription endpoint
- Browser-based FFmpeg.wasm MP4 render attempt

## Requirements
Install Node.js LTS from https://nodejs.org/ and use VS Code.

## Start the app
1. Extract the ZIP and open the `substudio` folder in VS Code.
2. Open Terminal → New Terminal.
3. Run `npm install`.
4. Run `npm run dev` and open the local URL, usually http://localhost:5173.

Editing, styling, animation preview and SRT/VTT export work without an API key.

## Set up Google Gemini API
1. Create a Gemini API key at https://aistudio.google.com/apikey.
2. Open a second terminal in the project folder and run `npm run server`.
3. Keep both the web app and API server running.
4. Paste the key into the **Gemini API key** field in the AI tools panel, or optionally add it as `GEMINI_API_KEY` in a `.env` file in the project root. The entered key stays in browser memory for the current session and is sent to the local API server, which uses it to authenticate with Gemini.
5. Upload a short video and click **Generate subtitles with AI**. The app uses FFmpeg.wasm to extract WAV audio in the browser, then sends it to the local server and Gemini API.

The starter upload limit is 18 MB for extracted audio. Longer media may exceed this and will need chunking. API availability, model access, quotas, and billing depend on your Google AI Studio/Gemini account. The model returns estimated cue timestamps, so review and adjust them before export. Your audio is sent to Google when you run transcription.

## Video export and animation
The MP4 render button uses FFmpeg.wasm and can be slow or fail for large files/codecs. The current animated presets are live preview effects; SRT/VTT formats do not store visual animation, and the MP4 export currently burns static subtitles. Animated rendering is a planned next step.

## Roadmap
1. Improve transcription timing, add chunked audio uploads and error handling.
2. Add draggable timeline, waveform, split/merge and keyboard shortcuts.
3. Render animations into MP4 with ASS/libass subtitle effects or frame-based rendering.
4. Add word-level karaoke timing, more templates and custom fonts.
5. Add local project save/load, then optional user accounts/cloud projects.
6. Add production security, rate limits, privacy policy, tests and deployment.

## Production build
`npm run build`

Keep API secrets server-side. This is a starter project, not yet a production service.
