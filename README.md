# StreamSync-Collaborative-AI-Video-Summarizer

Description
A web app that enables users to upload or link long videos (e.g. lectures, podcasts, webinars) and get AI-generated chapter breakdowns, summaries, and searchable transcripts. Users can collaborate to refine chapters and annotate key moments.

## Tech Stack
- Express.js (Node.js web server and front-end routing)
- ASP.NET Core (Collaborative annotation API and real-time features)
- Python (AI microservice for transcription and summarization)

## Requirements
- Transcript generation from video/audio (Hint: Use Whisper or an external transcription API)
- AI chapter and summary generation (Hint: Use LLMs with prompt templates for structured output)
- Collaborative annotation system (Hint: Store user contributions per timestamp)

## Installation
1. Clone the repo:
   bash
   git clone https://github.com/your-username/StreamSync-Collaborative-AI-Video-Summarizer.git
   cd StreamSync-Collaborative-AI-Video-Summarizer
   
2. Create environment files (`.env` or `appsettings.Development.json`) with your API keys and connection strings:
   bash
   # Root .env
   OPENAI_API_KEY=your_openai_api_key
   TRANSCRIPTION_API_KEY=your_transcription_api_key

   # ai-service/.env
   WHISPER_MODEL=base
   FLASK_ENV=development

   # annotation-api/appsettings.Development.json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=...;Database=...;Trusted_Connection=True;"
     },
     "JWT": {
       "Secret": "your_jwt_secret"
     }
   }
   
3. Install and run each service:
   - Python AI Service:
     bash
     cd ai-service
     python3 -m venv venv
     source venv/bin/activate
     pip install -r requirements.txt
     flask run --port 5001
     
   - ASP.NET Core Backend:
     bash
     cd annotation-api
     dotnet restore
     dotnet run --urls http://localhost:5002
     
   - Express.js Front-end Server:
     bash
     cd web-app
     npm install
     npm start
     

## Usage
1. Open your browser and navigate to http://localhost:3000.
2. Upload a video file or paste a video URL.
3. Wait for the transcript and AI-generated chapters & summaries.
4. Browse chapters and click to jump to key moments.
5. Add, edit, or delete annotations in real time with collaborators.
6. Search within the transcript using the search box.

## Implementation Steps
1. Scaffold the Express.js web-app for file uploads and front-end routing.
2. Build a Python Flask microservice using Whisper or an external API for transcription.
3. Integrate an LLM (e.g. OpenAI) for chapter and summary generation via prompt templates.
4. Develop an ASP.NET Core API with SignalR for collaborative annotations and real-time updates.
5. Configure a database (e.g. SQL Server) and define models for videos, transcripts, chapters, and annotations.
6. Wire up the front-end to consume each microservice’s endpoints and render the UI.
7. Implement user authentication and authorization using JWT tokens in ASP.NET Core.
8. Add live broadcasting of new annotations and chapter edits.
9. Write unit and integration tests for all services.

## API Endpoints
### Express.js (web-app)
- GET `/` – Serve the front-end application.
- POST `/api/upload` – Upload a video file.
- POST `/api/link` – Submit a video URL for processing.

### Python Flask (ai-service)
- POST `/transcribe` – Accepts video file or URL, returns a transcript JSON.
- POST `/summarize` – Accepts transcript, returns structured chapters and summaries.

### ASP.NET Core (annotation-api)
- GET `/annotations/{videoId}` – List all annotations for a video.
- POST `/annotations` – Create a new annotation.
- PUT `/annotations/{id}` – Update an existing annotation.
- DELETE `/annotations/{id}` – Remove an annotation.