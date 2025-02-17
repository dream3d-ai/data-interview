# Take-Home Assignment: Video Processing Pipeline

## Overview

In this assignment, you will design and implement a video processing pipeline that operates on the `validation` split of the [Kinetics dataset](https://github.com/cvdfoundation/kinetics-dataset), orchestrated by [Ray Data](https://docs.ray.io/en/latest/data/data.html). Assume each node has 32GB of RAM and 8 CPU cores. The pipeline should perform the following steps:

1. **Download Videos:**  
   Efficiently download videos from a provided list of URLs using an HTTP client (e.g., `aiohttp`).

2. **Transcode Videos and store in Lance format:**  
   Aggregate metadata and video data and store it in a dataset in the [Lance format](https://lancedb.github.io/lance/index.html). Use `pyav` to transcode each downloaded video to 360p. Use your discretion on how to store the transcoded videos. Please explain your reasoning. The video data will be used in a pytorch dataloader which will decode the video on the fly.

3. **Extra: Depth Map Extraction:**  
   Use a pre-trained monocular depth estimation model to extract a depth map from each video frame, and store it as a column in the Lance dataset. Again, explain your reasoning for your choice of model and how the extracted depth maps will be stored.

4. **Distributed Processing with Ray:**  
   Use [Ray Data](https://docs.ray.io/en/latest/data/data.html) to distribute the processing tasks (e.g., downloading, transcoding, and depth extraction) across workers. This distributed approach should help improve processing efficiency, especially when working with a larger set of data.

## Deliverables

- **Code Implementation:**  
  Provide a working implementation of the pipeline using Python. Your solution should be organized into logical modules (e.g., downloading, transcoding, depth extraction, data storage) and must incorporate Ray for distributed execution of tasks.

- **Documentation:**  
  Include a README (this file) that explains how to set up, run, and test your project. Document any assumptions or design decisions you made.

- **Testing:**  
  Include basic error handling and, where appropriate, unit tests for your individual modules. (Note: full test coverage is not mandatory, but quality and resilience of the implementation are important.)

## Setup Instructions

- Install [FFmpeg](https://ffmpeg.org/) and ensure it is available in your system's `PATH`.
- Install [UV](https://docs.astral.sh/uv/).
- Install the dependencies using UV `uv sync`.

## Additional Notes

- **Assumptions:** Clearly state any assumptions made, such as the format of the input URLs or the choice of resolution.
- **Enhancements (Optional):**
  - Consider implementing retries for failed downloads.
  - Although using Ray is required, you can explore additional optimizations in task distribution.
  - Write a brief summary of potential improvements if this were a production-level system.

Good luck, and we look forward to reviewing your implementation!
