- Qwen2.5-1.5B-Instruct is about 1.5 billion parameters. At fp16 (2 bytes each) the weights alone are about **3** GB. At int8 (1 byte each) about **1.5** GB.
  > fp16: 1.5*2 = 3 billion bytes. int8: 1.5*1 = 1.5 billion bytes
- Resident VRAM at 512 context, fp16: **4-5** GB. At 4096 context, fp16: **6-7** GB. (Which is larger, and by roughly how much?)
  > because it includes Cuda overhead + KV cache + model weights etc. For the 4096 context it is larger by 8 since 4096/512 = 8 so it's much larger because of the KV cache that holds the number of tokens, say KV cache * 8.
- During a single-request decode (one prompt, generating tokens one at a time), GPU utilisation will read about **98** percent.
  > because the GPU resources isn't fully saturated.
