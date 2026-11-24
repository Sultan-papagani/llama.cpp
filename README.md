# llama.cpp

![llama.cpp](https://raw.githubusercontent.com/ggml-org/llama-brand/refs/heads/master/logo/svg/cover/llama-cpp/cover-llama-cpp-dark.svg)

<div align="center">

This is based on llama.cpp version 1.0.0-dev (build 12522, commit `2cbfc3cf3`), with modifications that make Qwen 3.6 35B-A3B (any quant) loop through a section of its middle layers twice.

Specifically, layers **20–27 are executed twice**, while layers **0–19 and 28–39 run normally**. The second pass reuses the same layer weights but uses a separate memory bank for its attention and recurrent states, rather than simply feeding the layers through the exact same state twice.

The idea is to give the model more processing depth without adding or changing any model weights. Essentially, it gets another pass through part of its existing transformer network before continuing to the final layers.

In my own testing, the improvement is definitely noticeable. It's still experimental, and results can vary depending on the prompt, but I've seen more consistent reasoning and fewer obviously poor answers compared to the unmodified model.

**If you're VRAM-poor and already running this model, you should 1000% give this version a try. I think you'll notice the difference.**

</div>

---
