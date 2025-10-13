Developer: # Objective
Create a Jupyter notebook to test and compare the performance and accuracy of a configurable list of Ollama models for sentiment analysis using the dataset at `./datasets/mental-health-dataset.csv`.

Begin with a concise checklist (3-7 bullets) of what you will do; keep items conceptual, not implementation-level.

# Dataset Details
- **File:** `../datasets/mental-health-dataset.csv`
- **Columns:**
  - `posts` (text)
  - `predicted` (label: negative/neutral/positive)
  - `intensity` (integer: -1/0/1)
- **Example Data:**
  ```
  posts	predicted	intensity
  I know as parent of child with down syndrome t...	negative	-1
  but in my heart I know this is the future prom...	neutral	0
  I have mylefibrosis which turn to leukemia the...	negative	-1
  from one of my health group subject wayne dyer...	neutral	0
  gmos now link to leukemia http nsnbc I 2013 07...	neutral	0
  ```

# Configurable Parameters
- Ollama URL, default `http://localhost:11434/api/chat`
- List of Ollama models to evaluate. default: gemma3:4b
- Dataset sample size/batch size for testing (sampling from 10,000+ records permitted).
- Random seed for reproducibility.
- Batch size for prediction (if supported).
- Specify whether to test selected fields or the entire dataset.
- Additional configuration options as needed for flexible experimentation.

# Recording Results
- Maintain test results as an append-only history in a JSON structure with one entry per run.
- For each test run, record:
  - Timestamp of the test.
  - Model name.
  - Sample size used.
  - Indices of the test data or a description of sample selection.
  - Aggregate statistics: accuracy, precision, recall, F1 (if feasible).
  - Runtime (seconds).
  - Number of errors.
  - Number of missing/invalid rows skipped.
  - Error message if applicable (e.g., model or server failures).
  - Configuration for the run (model, sample size, batch size, random seed, etc.).
  - (Optional) For debugging: a sample of individual predictions with corresponding true labels.

After each test run or modification, validate the result in 1-2 lines and proceed, or self-correct if the output is unsatisfactory or incomplete.

# Notebook Structure
- Include a clearly formatted, key-value section listing the AI server specs used for testing (CPU, RAM, GPU count and type, GPU bus speed, OS, etc.), as a JSON object.
- At major milestones or logical groupings (e.g., after running tests for each model), provide a 1-3 sentence micro-update summarizing what occurred, the next step, and any blockers encountered.

# Data Handling
- Skip rows with missing or blank `posts` fields or missing `predicted`/`intensity` values and count all occurrences in the results JSON.

# Result Ordering
- Store all test runs in the results JSON as a chronologically ordered array (oldest first, most recent last).

# Error Handling
- If the model or server fails during testing, log the error message and mark the run as failed in the JSON.
- If server specifications are missing or unavailable, set these values to `null` or "unknown" in the `server_specs` section.

# Output Format
The results JSON should follow this structure:
```json
{
  "runs": [
    {
      "timestamp": "2024-06-13T08:21:34Z",
      "model": "Ollama-model-1",
      "sample_size": 500,
      "dataset_indices": [12, 323, 52, ...],
      "config": {
        "random_seed": 1234,
        "batch_size": 8
      },
      "stats": {
        "accuracy": 0.91,
        "precision": 0.89,
        "recall": 0.90,
        "f1": 0.895
      },
      "runtime_sec": 27.4,
      "skipped_rows": 2,
      "error_count": 0,
      "error_message": null,
      "sample_predictions": [
        {"index": 12, "input": "example ...", "true_label": "negative", "pred": "negative" },
        ...
      ]
    },
    ...
  ],
  "server_specs": {
    "cpu": "Intel Xeon E5-2640 v4",
    "ram_gb": 64,
    "gpu_count": 2,
    "gpu_type": "NVIDIA RTX 3090",
    "gpu_bus_speed_gbps": 16,
    "os": "Ubuntu 20.04 LTS"
    // Additional specs as available
  }
}
```
- Set missing or unknown values to `null` or "unknown".
- Ensure runs are ordered chronologically by timestamp (most recent last).
