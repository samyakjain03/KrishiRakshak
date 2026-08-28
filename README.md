# KrishiRakshak Edge

"Smart insights for healthier crops and resilient farms."

An AI-powered smart farming assistant for Indian farmers designed with an offline-first architecture to detect crop diseases, pests, nutrient deficiencies, water stress, and irrigation needs using Edge AI.

## Implemented Features
- **Responsive Landing Page**: Polished landing page demonstrating features and responsible AI guidelines.
- **Farmer Dashboard**: Real-time overview of crop health, soil moisture, and weather risk.
- **Crop Scanning (Mock Edge AI)**: Multi-step process to capture/upload crop images, presenting confidence, severity, and recommendations, and highlighting low-confidence cases for expert review.
- **Irrigation Management**: Decision support logic utilizing soil moisture trends and upcoming weather.
- **Alerts & Climate Risk**: Filterable alerts and climate risk indicator panel.
- **Advisory Assistant**: Chat-based interface with voice synthesis, language selection, and verified AI disclaimers.
- **Expert Dashboard**: Multi-farm overview with pending reviews and analytical charts.
- **Offline-First UI Guidelines**: Persistent connection status banners and sync queues.

## Mock Features
- Edge AI inference is currently mocked via `api.ts`.
- Real-time weather and sensor data are seeded from `mockData.ts`.
- Multilingual translation currently uses simulated logic on the frontend.
- Offline storage (IndexedDB) is conceptually designed but simulated via local state.

## Project Structure
- `/src/pages/farmer/*`: Farmer workflows (Dashboard, Scan, Irrigation, Alerts, Advisory)
- `/src/pages/expert/*`: Expert analytical dashboard
- `/src/components/*`: Reusable UI components (AppShell, AlertCard)
- `/src/services/api.ts`: Abstraction layer for AI and data fetching
- `/src/services/mockData.ts`: Seeded offline demo data
- `/src/types.ts`: Core data interfaces

## Setup Instructions

1. Install dependencies:
   ```bash
   npm install
   ```

2. Start the development server:
   ```bash
   npm run dev
   ```

3. The application will be available at `http://localhost:3000`.

## Connecting a Real Edge AI Model

Currently, `analyzeCropImage` in `src/services/api.ts` uses a setTimeout mock. To connect a real TensorFlow Lite or ONNX model:

1. Import the appropriate WebAssembly or JS runtime (e.g., `@tensorflow/tfjs` and `@tensorflow/tfjs-tflite`).
2. Pre-load your model into browser cache/IndexedDB during the application bootstrap phase for offline access.
3. In `analyzeCropImage`, convert the captured image blob to a tensor.
4. Run `model.predict(tensor)` and map the output logits to the required `CropScan` interface (diagnosis, confidence, severity).
5. Ensure the inference block is wrapped in a try/catch, falling back to network-based inference if the device cannot support Edge AI.

## Deployment to Vercel

1. Push your repository to GitHub.
2. Log in to Vercel and create a new Project.
3. Import the GitHub repository.
4. Ensure the Framework Preset is set to "Vite".
5. Click **Deploy**. Vercel will automatically run `npm run build` and host the static files.

## Environment Variables

Copy `.env.example` to `.env` and configure any required external APIs if extending the mock functionalities. For this frontend prototype, no external API keys are required to run the demo.
