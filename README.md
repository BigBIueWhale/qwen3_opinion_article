# 💪 Qwen3-32b is **THE BEST**

🧙‍♂️ Since Github Copilot introduced in 2022, I've wanted a good LLM to use locally for coding, engineering and math.

🤗 Thankfully, we now have an open-weights model: `Qwen3-32B`, which runs locally and outperforms `GPT-o1` at coding and math.

## 😮 Qwen3 Gotchas

- 💬 Qwen3 works well in English and Chinese. For example `Gemma3-27b` has much better multilingual performance.

- ⚙️ Specific inference parameters must be requested with each API query to Ollama / llama.cpp:
    | Parameter        | Value                                                           |
    | :--------------- | :-------------------------------------------------------------- |
    | `Context Length` | 11000                                                           |
    | `num_predict`    | -1                                                              |
    | `Temperature`    | 0.6                                                             |
    | `Top K`          | 20                                                              |
    | `Top P`          | 0.95                                                            |
    | `Min P`          | 0                                                               |
    | `Repeat Penalty` | 1                                                               |
    | `num_gpu`        | 65                                                              |

- 📚 On a 24GB VRAM GPU, we can only squeeze 11000 token context length. Which requires 4-bit model quantization and 8-bit KV-cache quantization.\
If you do have more VRAM- you can utilize the full 32,768 tokens and leave the KV-cache at its natural 16-bit precision.

## 🧪 Qwen3 Secret Sauce

- 🚀 `Qwen3-32B` is fast! Runs at ~27 tokens per second on an Nvidia A5000 GPU with 24GB VRAM (~400 tok/s prompt ingestion speed). See full guide: https://github.com/BigBIueWhale/openwebui_config.

- 🤯 Qwen3 models were pre-trained on 36 trillion tokens. More than double the 14.8 trillion tokens in Deepseek V3's pretraining data.

- 🧠 Qwen3 was trained in full 16-bit precision. That's 4x more expensive than Deepseek's approach to do 8-bit precision training- but also yields greater quality for the same model size.

- 📚 Qwen3 offers 32,768 token context length without quality loss (max 131,072 token context with YaRN).

- 😤 Qwen3 is much better at avoiding overthinking than `QwQ-32B` and the original `Deepseek-R1`.

- 🤖 `Qwen3-32B` and `Qwen3-235B-A22B` were post-trained to think using pure RL without human feedback, based on synthetic data. See "Long-CoT Cold Start" and "GRPO" in [Qwen3 Technical Report](https://arxiv.org/pdf/2505.09388).

- 🔨 Qwen3 supports tool-calling with Model Context Protocol (MPC).

- 😎 Option to turn off thinking (sacrificing response quality).

- 🤡 Note: `Qwen3-30B-A3B`, `Qwen3-14B` and smaller Qwen3 models are (shockingly) stupid. Knowledge distillation (strong to weak) just doesn't seem to work very well. The Qwen team tried to perform the full post-training on `Qwen3-14B` / `Qwen3-30B-A3B` and remarkably found that it performed even worse than distillation strong-to-weak. This experiment uncovered a scaling law!\
`Qwen3-32B` base model unlocked an ability that the smaller models simply couldn't learn.

## 🏛️ Historic Breakdown

- 🤠 **November 30, 2022**- OpenAI released ChatGPT, based on "original gangster" `GPT-3` base model with 175 billion, and 2048 token context length.

- 🦸‍♂️ **March 3, 2023**- `Meta LLaMA` 65 billion parameters, 33B, 13B, and 7B models were leaked on 4chan. LLaMA outperformed GPT-3 on all tasks, Chinchilla on all but one, and PaLM on all but two.

- 👑 **March 14, 2023**- OpenAI released GPT-4, a MoE (mixture of experts) 1.76 trillion parameter model. It has 16 experts, each with 110 billion parameters. The purpose is to allow the model to be huge (lots of knowledge) and circumvent the square law of training cost- normally doubling the parameters requires 4x the compute.

- 👟 **November 17, 2023**- OpenAI CEO Sam Altman was ousted from OpenAI (briefly). Theories say the reason was his apparent disregard for safety when handling OpenAI's internal, newly-developed "dangerous" LLM with business partners (Microsoft). This mystery LLM was trained to efficiently reason (think) before answering. This top-secret algorithm was known at the time as Q* (Q Star) / Strawberry (according to leaks).

- 🎨 **May 29, 2024**- Mistral AI released `Codestral-22B`- the first open-weights model that's decent at coding tasks (routinely produces code that actually works), with 32k token context. This model gave me hope for open source.

- 👑 **December 5, 2024**- OpenAI finally released `GPT-o1`- a thinking model. Huge quality gain in instruction following compared to previous SoTA GPT-4. OpenAI's moat widens.

    > "Goodbye, GPT-4. You kicked off a revolution. We will proudly keep your weights on a special hard drive to give to some historians in the future." — Sam Altman

- 🫠 **December 28, 2024**- Alibaba's Qwen team released the weights for `QwQ-32B-Preview`- the first with thinking abilities. Sadly this release was rushed, and it's wasn't capable of generating working code.

- 🐳 **January 20, 2025**- China's Deepseek released the weights of `Deepseek R1`- a 671 billion parameter (over)thinking model that approaches GPT-o1's coding ability. Based on a fully-open source newly-developed architecture that allows for cheap pretraining- they pioneered stable 8-bit training (4x less cost), and optimized training code for Nvidia GPUs. Deepseek V3 base model was designed to be so cheap at training and inference, that the company still serves the full model on their website for free!

- 🤔 **March 5, 2025**- Alibaba's Qwen team released `QwQ-32B` Alibaba proved that "thinking is all you need". They trained a 32 billion parameter model to think ~6000+ tokens before every response, and remarkably got benchmark performance equivalent to or surpassing full Deepseek-R1-671B! Even outperforming GPT-o1 on math benchmarks. Finally we had a GPT-o1 alternative that is small enough to run on a 24GB VRAM GPU!\
Initially, the open source community thought Alibaba is lying about the benchmarks, but then some reddit users realized that the inference parameters need to be adjusted for optimal performance.

- 🖼️ **March 12, 2025**- Google releases the weights of `Gemma3-27B`- a truly multilingual LLM with native image understanding. The catch? Gemma3 is shockingly bad at knowledge, coding, math tasks and recalling conversation context.

- 💪 **April 29, 2025**- Alibaba's Qwen team released two flagship models `Qwen3-32B`, `Qwen3-235B-A22B`. A godsend for local LLM users. Alibaba is proud of their "flagship models". They poured love 💖 into the training.

- 🐳 **May 29, 2025**- A "minor" update was released- `DeepSeek-R1-0528`. The update is not minor at all. The new version of Deepseek R1 approaches GPT-o3 coding benchmark scores, and surpasses even `Qwen3-235B-A22B`. They fixed DeepSeek R1. Probably a response to being humiliated by Alibaba's Qwen3 flagship models.

- 👑 **June 17, 2025**- Google releases final (non-preview) version of `Gemini 2.5 Pro`. With a context length of 1 million tokens. This is the best coding model- able to one-shot entire applications. It doesn't perform as well as OpenAI O3 on benchmarks, and it's also not very good at following instructions- but it is the best at coding.

    > "At the end of the day, [Google is] the 800-pound gorilla in this"
    >
    > "I want people to know that we made Google dance." — Satya Nadella
