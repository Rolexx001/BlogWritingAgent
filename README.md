# BlogWritingAgent


An AI-based technical blog writer built with **LangGraph, Gemini, Tavily, and Streamlit**.

The project takes a technical topic as input and turns it into a structured Markdown blog. Depending on the topic, it can perform web research, collect relevant evidence, create a blog outline, generate sections in parallel, and add images or diagrams where they make sense.

## What it does

The workflow is designed around a few simple steps:

1. Takes a blog topic from the user.
2. Decides whether external research is needed.
3. Searches the web using Tavily when required.
4. Creates a structured blog plan.
5. Splits the plan into individual writing tasks.
6. Generates the sections in parallel using LangGraph.
7. Merges the generated sections in the correct order.
8. Decides whether images or diagrams would improve the article.
9. Generates the required images.
10. Produces the final Markdown blog.

## Features

- Technical blog generation with Gemini
- Conditional web research with Tavily
- Structured planning using Pydantic models
- Parallel section generation with LangGraph
- Markdown output
- Automatic image/diagram planning
- AI-generated images
- Streamlit-based interface
- Markdown preview
- Previous blog history
- Downloadable Markdown and blog bundle
- Execution logs and workflow progress
- Graceful handling of image generation failures

## Architecture

```text
                         User Topic
                             |
                             v
                         +-------+
                         | Router|
                         +---+---+
                             |
                 +-----------+-----------+
                 |                       |
                 v                       v
            +---------+            +-------------+
            | Research|            | Orchestrator|
            | Tavily  |            | Blog Plan   |
            +----+----+            +------+------+
                 |                        |
                 +-----------+------------+
                             |
                             v
                       Blog Plan / Tasks
                             |
                         Fan-out
                             |
              +--------------+--------------+
              |              |              |
              v              v              v
           Worker         Worker         Worker
              |              |              |
              +--------------+--------------+
                             |
                         Fan-in
                             |
                             v
                     Merge Sections
                             |
                             v
                      Decide Images
                             |
                             v
                     Generate Images
                             |
                             v
                     Final Markdown
