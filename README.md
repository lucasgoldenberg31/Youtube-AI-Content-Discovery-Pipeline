# YouTube AI Content Discovery Pipeline

This repository contains an n8n workflow that turns a YouTube playlist into a searchable music recommendation assistant powered by AI.

## Overview

The workflow:

- Loads a YouTube playlist
- Retrieves each video in the playlist
- Extracts metadata such as title, artist/channel, published date, and duration
- Stores the video information in an in-memory vector database
- Uses embeddings to enable semantic search over the saved content
- Exposes that database to an AI agent that answers user questions like:
  - "Recommend upbeat songs"
  - "Find slow and emotional tracks"
  - "Suggest songs similar to my playlist vibe"

This is implemented as an n8n workflow file in the project root.

## Included Workflow

- `Lab 6 Youtube Lab.json` — exported n8n workflow for the AI-powered YouTube playlist recommendation assistant

## How It Works

The workflow is structured as follows:

1. Manual trigger starts the process.
2. YouTube node retrieves playlist items for the configured playlist.
3. Video details are fetched for each item.
4. Video metadata is formatted into document text.
5. Google Gemini embeddings are generated for each document.
6. Data is stored in an in-memory vector store.
7. A chat-triggered agent uses the vector store as a tool to search the playlist.
8. A Gemini chat model responds to user prompts using the indexed content.

## Workflow Configuration

Before using the workflow, make sure the following are configured in n8n:

- YouTube OAuth2 credentials
- Google Gemini / PaLM API credentials
- Correct playlist ID in the `Get Playlist` node
- Correct model name in the Gemini chat node if needed

The playlist node currently uses:

`PL0EIKnMg-NhRdjfglbGWTyKTk7aij0gmC`

You can replace this with your own playlist ID.

## Requirements

- n8n
- YouTube API access
- Google Gemini API access
- An n8n instance with LangChain nodes enabled

## Example Use Cases

- Search your saved favorite songs by mood
- Ask for recommendations based on a theme or energy level
- Build a conversational music assistant around a curated playlist

## Importing the Workflow

1. Open n8n.
2. Go to your workflow dashboard.
3. Click Import.
4. Upload `Lab 6 Youtube Lab.json`.
5. Configure credentials and update the playlist ID if needed.
6. Activate the workflow.

## Notes

This project is a lightweight demo and uses an in-memory vector store, which is suitable for experimentation and local demos. For production use, you may want to replace it with a persistent vector database.

## License

This project does not currently include a license file. If you plan to share or distribute it publicly, consider adding an open-source license such as MIT.
