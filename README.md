# Shadow AI Domains

**A curated database of 188 AI service domains your employees can reach right now.**

---

Your network has hundreds of doors to AI services. Most of them are wide open.

This dataset catalogs AI service domains across LLM providers, SaaS platforms with embedded AI, multimodal generators, and voice/audio tools.  Every category of AI your security team should be tracking.

The goal isn't to block everything.  It's to know what's out there so you can make informed decisions instead of discovering shadow AI usage in your next incident review.

## Why This Matters

Free LLM providers are everywhere. Not five or ten. Dozens. Many require no account. Some require no API key. Your employees have access to all of them from any browser on your network.

That's the baseline. It gets worse.

**Aggregators bypass per-provider blocking.** OpenRouter provides a single API endpoint that routes to dozens of models from different providers. Block OpenAI, Anthropic, and Google individually? Your users can still reach all three through one domain. Poe does the same thing through a consumer interface.

**Open source inference platforms eliminate the provider entirely.** Hugging Face, Replicate, RunPod, Vast.ai. Anyone can spin up a model with zero oversight. No terms of service. No usage logging. No audit trail.

**Chinese and Russian providers operate under different data governance regimes.** DeepSeek, Alibaba Qwen, Baidu ERNIE, ByteDance Doubao, Yandex, Sberbank GigaChat. Several are on the US entity list. Data submitted to these services may be subject to foreign government access requirements. That's not speculation. That's their legal framework.

**Your existing SaaS tools are embedding AI silently.** Salesforce Einstein. Zoom AI Companion. Slack AI. Teams Copilot. Notion AI. These aren't separate services you can isolate. Block the domain and you break the tool. Your employees may be sending sensitive data through AI features they didn't even know were active.

How do you stop data exfiltration when the AI is baked into the productivity tool?

## Dataset Overview

| File | Entries | Coverage |
|------|---------|----------|
| `llms.csv` | 123 | LLM providers, cloud AI endpoints, aggregators, dev tools, open source inference, AI search |
| `saas.csv` | 52 | Enterprise SaaS with embedded AI features (CRM, productivity, meetings, HR, support) |
| `multimodal.csv` | 8 | Image and video generation |
| `voice.csv` | 5 | Voice cloning and music generation |

**188 total entries** across all files.

## CSV Schema

Every file follows the same structure:

| Column | Description |
|--------|-------------|
| `Domain` | The domain or wildcard pattern (e.g., `*.openai.com`) |
| `Category` | Primary classification (e.g., Frontier / Consumer, Cloud Provider AI) |
| `Subcategory` | Provider or function grouping (e.g., OpenAI, Hugging Face, CRM / Sales) |
| `Country` | Country of origin or primary operation |
| `Notes` | Operational context, blocking warnings, entity list flags |

## Categories

**LLMs & AI Platforms**
- Frontier / Consumer (OpenAI, Anthropic, Google, Mistral, DeepSeek, xAI, Cohere, and more)
- Cloud Provider AI (Azure OpenAI, AWS Bedrock, Google Vertex, Together AI, Groq, Cerebras, SambaNova)
- Aggregators / Wrappers (OpenRouter, Perplexity, Poe, Character AI, Meta AI)
- Open Source Inference (Hugging Face, Replicate, Modal, RunPod, Vast.ai, Ollama)
- Dev Tooling / IDE (GitHub Copilot, Cursor, Codeium, Tabnine, Replit, Sourcegraph Cody)
- Productivity / Workflow (Notion AI, Grammarly, Jasper, Otter.ai, Glean)
- Agent / Orchestration (LangChain, LlamaIndex, Dust)
- Search / AI Search (Kagi, Exa, Bing AI)

**SaaS / Enterprise**
- CRM / Sales (Salesforce, HubSpot, Apollo, Gong, Clay)
- Productivity / Automation (Zapier, Airtable, Monday, Asana, ClickUp)
- Communication / Meetings (Zoom, Teams, Slack, Fireflies, Otter.ai, Fathom)
- HR / Recruiting (Workday, Greenhouse, Lever, Paradox)
- Document / Knowledge (Box, Dropbox, DocuSign, Adobe, Glean)
- Data / Analytics (Tableau, Power BI, Hex, ThoughtSpot, Scale AI)
- Customer Support (Intercom, Zendesk, ServiceNow, Freshworks, Ada, Moveworks)
- Content / Writing (Writer)
- Agent / Automation (Adept)

**Multimodal**
- Image / Multimodal (Midjourney, Stability AI, Ideogram, Runway, Pika, Sora, Kling, Hailuo)

**Voice / Audio**
- Voice cloning (ElevenLabs, Murf, Play.ht)
- Music generation (Suno, Udio)

## Geographic Coverage

Domains span **11 countries**: USA, China, France, Israel, Canada, Germany, UK, Russia, UAE, Finland.

A few things worth flagging:

- **US Entity List.** SenseTime, iFlytek, and related domains are on the US Bureau of Industry and Security entity list. Interactions with these services may have export control implications.
- **Defense Context Reviews.** UAE-based providers (Falcon LLM / TII, AI71, Core42) are flagged for defense context review in the dataset.
- **Russian Providers.** Yandex and Sberbank operate under Russian data localization laws. Data submitted may be stored and accessible within Russian jurisdiction.
- **Chinese Providers.** 20+ domains from Chinese providers including DeepSeek, Alibaba, Baidu, ByteDance, Tencent, Zhipu AI, Moonshot, MiniMax, 01.AI, Qihoo 360, SenseTime, iFlytek, and BAAI. Data governance follows PRC regulations.

## Usage Notes

**Wildcard domains.** Most entries use `*.example.com` format for comprehensive blocking. This catches subdomains like `api.example.com` and `cdn.example.com` that would otherwise slip through.

**"Review before blocking" warnings.** Several SaaS entries include explicit warnings. Salesforce, Zoom, Slack, Teams, Workday, ServiceNow, Box, Dropbox, DocuSign, Adobe, Tableau, Power BI, Zendesk, and Notion all have AI features embedded in domains your org depends on. Blocking these domains will break the underlying tool. You need a different strategy for these. Disable the AI features at the admin level where possible.

**OpenRouter is a single-endpoint bypass risk.** One domain. Access to dozens of models from multiple providers. If you're blocking AI providers individually and not blocking OpenRouter, you have a gap.

**Cloud provider AI endpoints overlap with legitimate services.** Azure OpenAI, AWS Bedrock, and Google Vertex AI run on the same infrastructure as your production workloads. Blocking `*.openai.azure.com` may affect legitimate Azure services. Handle these with network policies or conditional access, not blanket domain blocks.

**Bing AI.** Blocking `*.bing.com` will break Bing search entirely. Review before applying.

## Contributing

PRs welcome. Follow the existing CSV format:

```
Domain,Category,Subcategory,Country,Notes
```

When adding entries:
- Use wildcard format (`*.example.com`) where the provider uses subdomains
- Include the country of origin
- Add operational notes, especially "review before blocking" warnings for services that share domains with non-AI functionality
- Place entries in the appropriate CSV file based on primary function

## License

MIT
