# Take-Home Assignment: Video Processing Pipeline

## Overview

In this assignment, you will design and implement a highly-parallel video processing pipeline that operates on the `validation` split of the [Kinetics dataset](https://github.com/cvdfoundation/kinetics-dataset). The pipeline should perform the following steps:

1. **Download Videos:**  
   Efficiently download videos from a provided list of URLs using an HTTP client (e.g., `aiohttp`). For testing, you can limit the data to the first shard.

2. **Transcode Videos and store in Lance format:**  
   Aggregate metadata and video data and store it in a dataset in the [Lance format](https://lancedb.github.io/lance/index.html). You should transcode each downloaded video to 360p. Use your discretion on how to store the transcoded videos. Please explain your reasoning. The video data will be used in a pytorch dataloader which will decode the video on the fly.

3. **Important: Parallelism**  
   The dataset consists of many large shards, requiring an efficient parallel processing strategy. Consider the different levels of parallelism—such to optimize each stage of the pipeline. You are free to choose any concurrency model, but ensure that the approach is scalable and fault-tolerant. [Ray](https://docs.ray.io/en/latest/?_gl=1*azgm7f*_gcl_au*MTE5MjAyNjI3MC4xNzM5NTYxNjQ3) is an option for task distribution and resource management across multiple workers.

4. **Optional**: Depth Map Extraction:
Use a pre-trained monocular depth estimation model to extract a depth map from each video frame, and store it as a column in the Lance dataset. Again, explain your reasoning for your choice of model and how the extracted depth maps will be stored.


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
