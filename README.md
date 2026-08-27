# YouTube Video Summarizer & Q&A

A Gradio app that takes a YouTube video URL, pulls its transcript, and lets you:

- **Summarize** the video in a concise paragraph
- **Ask questions** about the video's content, answered using retrieval over the transcript (chunked + embedded + searched with FAISS)

## How it works

1. Fetches the video transcript via `youtube-transcript-api` (prefers a manually-created transcript over an auto-generated one).
2. For summarization, the full transcript is passed directly to the LLM.
3. For Q&A, the transcript is chunked, embedded, and indexed with FAISS so only the most relevant passages are sent to the LLM along with the question.
4. Both flows run on an IBM watsonx.ai foundation model (`ibm/granite-8b-code-instruct` for generation, `ibm/slate-30m-english-rtrvr-v2` for embeddings) via LangChain.

## Setup

```bash
pip install -r requirements.txt
```

Set your watsonx.ai credentials as environment variables:

```bash
export WATSONX_URL="https://us-south.ml.cloud.ibm.com"
export WATSONX_PROJECT_ID="<your-project-id>"
```

## Run

```bash
python main.py
```

Opens a Gradio interface at `http://localhost:7860` — paste a YouTube URL, then summarize or ask questions about the video.
