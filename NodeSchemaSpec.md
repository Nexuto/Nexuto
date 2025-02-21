# AI Node Schema Specification

## Overview
This document defines the schema for AI nodes in a drag-and-drop AI platform. It ensures that the hub can dynamically display, validate, and manage connections between AI tools.

## Node Schema
Each AI node should declare its inputs, outputs, and connection rules using the following JSON structure:

```json
{
  "node_id": "text_summarizer_001",
  "name": "Text Summarizer",
  "description": "Summarizes input text into a shorter version.",
  "category": "NLP",
  "inputs": [
    {
      "socket_id": "input_1",
      "name": "Text Input",
      "type": "text",
      "multiple": false,
      "required": true
    }
  ],
  "outputs": [
    {
      "socket_id": "output_1",
      "name": "Summary Output",
      "type": "text",
      "multiple": true
    }
  ],
  "settings": {
    "max_length": {
      "type": "integer",
      "default": 100,
      "min": 10,
      "max": 500
    }
  }
}
```

### Fields Explanation
- **`node_id`**: Unique identifier for the AI tool.
- **`name`**: Display name of the node.
- **`description`**: Brief explanation of the node’s function.
- **`category`**: Categorizes nodes (e.g., NLP, Image Processing, Audio Analysis).
- **`inputs`**: Defines acceptable inputs:
  - **`socket_id`**: Unique ID for the input socket.
  - **`name`**: Display name for UI.
  - **`type`**: Data type (`text`, `image`, `audio`, etc.).
  - **`multiple`**: Whether multiple connections are allowed.
  - **`required`**: Specifies if the input is mandatory.
- **`outputs`**: Defines the node’s outputs:
  - Same structure as `inputs` but specifies what the node produces.
- **`settings`**: Optional parameters users can configure.

## Connection Schema
To enable node connectivity, the platform should define connections as follows:

```json
{
  "connection_id": "conn_789",
  "from": {
    "node_id": "text_summarizer_001",
    "socket_id": "output_1"
  },
  "to": {
    "node_id": "sentiment_analyzer_002",
    "socket_id": "input_1"
  }
}
```

### Connection Rules
- **Only compatible types can connect** (`text` → `text`, `image` → `image`).
- **Multiple outputs can connect to multiple inputs.**
- **Circular dependencies should be avoided.**

## Implementation Considerations
- The UI should enforce **real-time validation** of connections.
- The execution order should follow **dependency graphs**.
- Nodes should support **parallel processing where applicable**.
