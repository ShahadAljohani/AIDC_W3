- Time to first token (TTFT) is dominated by prefill (reading the whole prompt). A longer prompt makes TTFT go **up** (up / down / no change).
 > because it has to process the first token.
- After the first token, decode emits one token at a time. The mean gap between tokens (TPOT) depends mostly on model size and MEM bandwidth (prompt length / model size and memory bandwidth).
 > because it is a decoding process in which it streams the tokens so it depends on the model size and how fast the weights move
- KV cache math for Qwen2.5-1.5B: 28 layers, 2 KV heads, head_dim 128, fp16. Per token that is 2 (K and V) x 28 x 2 x 128 x 2 bytes = **28** KB per token. So a 4096-token context holds about **0.11** GB of KV. (Compute it; do not guess.)
 > KB = 1024 B so I divided (after multiplying) by 1024   => 28672/1024 = 28 KB. and GB=1024^2 KB so 28*4096 = 114688   => 114688/(1024^2) ~ 0.11
- Static batching: if you pad 8 prompts of different lengths and run them as one batch, the batch finishes when the **slowest** prompt finishes.
