# AI Node Schema Specification

## Overview

This document defines the schema for AI nodes in a drag-and-drop AI platform. It ensures that the hub can dynamically display, validate, and manage connections between AI tools.

## Node Schema

Each AI node should declare its inputs, outputs, and connection rules using the following JSON structure:

```json
{
  "node_id": "text_summarizer_001",
  "name": "Node Name",
  "description": "Summarizes what the Node does",
  "category": "NLP",
  "inputs": [
    {
      "input_id": "input_identifier",
      "name": "Text Input",
      "type": "text",
      "required": true
    }
  ],
  "outputs": [
    {
      "output_id": "output_identifier",
      "name": "Text Input",
      "type": "text",
    }
  ],
}
```

### Fields Explanation

- **`node_id`**: Unique identifier for the node.
- **`name`**: Display name of the node.
- **`description`**: Brief explanation of the node’s function.
- **`category`**: Node category (e.g., NLP, Image Processing).
- **`inputs`**: Defines the node's required inputs:
  - **`input_id`**: Unique identifier for the input (from the JSON).
  - **`name`**: Input display name.
  - **`type`**: Expected data type (e.g., text, image).
  - **`required`**: Specifies if the input is mandatory.
- **`outputs`**: Defines the node's outputs:
  - **`output_id`**: Unique identifier for the output (from the JSON).
  - **`name`**: Output display name.
  - **`type`**: Output data type (e.g., text, image).

## Connection Schema

To enable node connectivity, the platform should define connections as follows:

```json
{
  "connection_id": "conn_789",
  "from": {
    "node_id": "text_summarizer_001",
  },
  "to": {
    "node_id": "sentiment_analyzer_002",
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
