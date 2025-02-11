# Take-Home Assignment: Kinetics Depth Extraction Pipeline

## Overview

In this assignment, you will design and implement a video processing pipeline that operates on the validation split of the Kinetics dataset, orchestrated by Ray. The pipeline will perform the following steps:

1. **Download Videos:**  
   Asynchronously download videos from a provided list of URLs using an HTTP client (e.g., `aiohttp`).

2. **Transcode Videos:**  
   Use FFmpeg to transcode each downloaded video to 360p.

3. **Depth Map Extraction:**  
   Use a pre-trained monocular depth estimation model to extract a depth map from each video frame.

4. **Data Storage in Lance Format:**  
   Aggregate metadata (such as video paths, the depth map path, and original source URL) and store it in a dataset in the Lance format (https://lancedb.github.io/lance/index.html).

5. **Distributed Processing with Ray:**  
   Use [Ray](https://www.ray.io/) to distribute the processing tasks (e.g., downloading, transcoding, and depth extraction) across workers. This distributed approach should help improve processing efficiency, especially when working with a larger set of data.

## Deliverables

- **Code Implementation:**  
  Provide a working implementation of the pipeline using Python. Your solution should be organized into logical modules (e.g., downloading, transcoding, depth extraction, data storage) and must incorporate Ray for distributed execution of tasks.

- **Documentation:**  
  Include a README (this file) that explains how to set up, run, and test your project. Document any assumptions or design decisions you made.

- **Testing:**  
  Include basic error handling and, where appropriate, unit tests for your individual modules. (Note: full test coverage is not mandatory, but quality and resilience of the implementation are important.)

## Technical Requirements

- **Downloading:**  
  Use asynchronous I/O (e.g., `aiohttp`) to enable parallel downloads.

- **Transcoding:**  
  Invoke FFmpeg through a subprocess call. Ensure FFmpeg is installed on your system and available in your `PATH`.

- **Depth Extraction:**  
  Use ml-depth-pro to process a representative frame of the video. If necessary, a simple version that extracts just the first frame (using OpenCV or similar) is acceptable.

- **Data Storage:**  
  Store the metadata records (video ID, file paths, source URL, etc.) in a Parquet file using PyArrow. This file represents a simplified version of the Lance format for the purpose of this project.

- **Distributed Processing:**  
  Use Ray to distribute tasks. Candidates should design the pipeline so that tasks (e.g., downloading, transcoding, and depth extraction) are executed in parallel using Ray's task and actor abstractions.

## Evaluation Criteria

Your submission will be evaluated based on the following considerations:

- **Correctness:**  
  Does the pipeline perform the required tasks correctly from video download through data storage?

- **Code Quality:**  
  Is the code well-structured, modular, and easy to read? Is error handling properly implemented? Are Ray's distributed processing capabilities effectively used?

- **Documentation:**  
  Is the README clear? Are instructions provided for setting up and running the project?

- **Engineering Judgment:**  
  How do you balance simplicity with production-like quality? Feel free to include improvements or explain decisions regarding design, error retry logic, or performance enhancements.

## Setup Instructions

1. **Prerequisites:**

   - Install [FFmpeg](https://ffmpeg.org/) and ensure it is available in your system's `PATH`.
   - Install [UV](https://docs.astral.sh/uv/).
   - Install the dependencies using UV `uv sync`.

2. **Running the Pipeline:**
   Provide clear instructions (e.g., `python main.py`) on how the candidate can run and test your implementation.

## Additional Notes

- **Assumptions:** Clearly state any assumptions made, such as the format of the input URLs or the choice of resolution.
- **Enhancements (Optional):**
  - Consider implementing retries for failed downloads.
  - Although using Ray is required, you can explore additional optimizations in task distribution.
  - Write a brief summary of potential improvements if this were a production-level system.

Good luck, and we look forward to reviewing your implementation!
