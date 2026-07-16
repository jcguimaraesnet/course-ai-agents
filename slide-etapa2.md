---
layout: section
routeAlias: etapa2
---
## **Etapa 2:** OpenAI Agents SDK 
**Entendendo o básico**

---
layout: default
sourceLabel: Install UV
source: https://docs.astral.sh/uv/getting-started/installation
---

# Diferença entre tipos de APIs da OpenAI

#### **A OpenAI evoluiu suas APIs ao longo do tempo**

<br/>

<Transform :scale="0.8">

| | Completions | Assistants | **Chat Completions API** | **Responses API** |
| --- | --- | --- | --- | --- |
| ano | 2020 | 2023 | 2023 | 2025 |
| endpoint | /v1/completions | /v1/assistants | `/v1/chat/completions` | `/v1/responses` |
| entrada | string | Threads Runs | messages[] `array` | items[] `array` |
| estado | stateless | stateful | *stateless* | *stateful* opcional |
| ferramentas | nenhuma | file/code | *nenhuma* | web, file, code, etc |
| status | legada | descontinuada | **suportada** | **recomendada** |

</Transform>


---
layout: two-cols-header
layoutClass: gap-8
sourceLabel: Install UV
source: https://docs.astral.sh/uv/getting-started/installation
---

# Chat Completions API vs Responses API

<!-- #### **O que acontece por debaixo do capô quando você roda Runner.Run(agent, ...)** -->


::left::

```python [Chat Completions API]
from openai import OpenAI

client = OpenAI()
resp = client.chat.completions.create(
    model="gpt-5",
    messages=[
        {"role": "system",
         "content": "Você é um professor."},
        {"role": "user",
         "content": "Qual a capital da França?"},
    ],
)
print(resp.choices[0].message.content)
```


::right::

```python [Responses API]
from openai import OpenAI

client = OpenAI()

resp = client.responses.create(
    model="gpt-5",
    instructions="Você é um professor.",
    input="Qual a capital da França?",
)

print(resp.output_text)
```

::bottom::

<Transform :scale="0.7" origin="top left">

> [!IMPORTANT]
> Os dois exemplos usam diretamente lib da OpenAI. <br/>
> O SDK Agents usa a lib da OpenAI.

</Transform>

---
layout: default
---

# Chat Completions API vs Responses API

#### **A importância das duas APIs**

<br/>

<v-clicks every="1">

- OpenAI Agents SDK usa por padrão a Responses API
- Praticamente nenhum provedor usa o padrão de Response API
- OpenAI definiu um formato (Chat Completions), e o mercado copiou (OpenAI-compatible).
- A API Chat Completions se tornou língua universal na industria (DeepSeek, Perplexity, OpenRouter, etc)
- Anthropic e Google oferecem outros formatos de API (com alguma compatibilidade com a Chat Completions API)
- **Para usar modelos não OpenAI, use obrigatoriamente a Chat Completions API**
- **Para usar modelos OpenAI, prefira a Responses API**

</v-clicks>

---
layout: two-cols-header
layoutClass: gap-8
sourceLabel: Ativando Chat Completions
source: https://openai.github.io/openai-agents-python/models/#responses-api-support
---

::left::

```python {all|5,7,15|all}{at:+1} 
import asyncio, os
from dotenv import load_dotenv
from agents import Agent, Runner, set_default_openai_api

os.environ["OPENAI_BASE_URL"] = "https://api.deepseek.com"

set_default_openai_api("chat_completions")

async def main():
    load_dotenv()

    agent = Agent(
        name="Assistant",
        instructions="You are a history professor.",
        model="deepseek-v4-fast"
    )

    result = await Runner.run(agent, 
        "What's the capital of France?")
    print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())
```


::right::

> [!TIP]
> O OpenAI Agents SDK permite **ativar/desativar** o uso da Chat Completions API para usar com outros modelos não OpenAI. 

<br/>

<v-clicks every="2" at="+1">

- O método `set_default_openai_api` precisa invocado
- As variáveis `OPENAI_API_KEY` e `OPENAI_BASE_URL` devem ser preenchidas com as informações do provedor não OpenAI.

</v-clicks>


---
layout: default
sourceLabel: API Google Pricing
source: https://ai.google.dev/gemini-api/docs/pricing
---

# Gateway/Provedores com API gratuita

#### **Plataformas do tipo agregador de provedores oferecem dezenas de modelos gratuitos**

<br/>

<Transform :scale="0.8">

| Provedor | Modelo (exemplo) | Plataforma | Cartão |
|---|---|---|---|
| Google | `gemini-3.5-flash` | [aistudio.google.com](https://aistudio.google.com) | não |
| Groq | `llama-3.3-70b-versatile` | [console.groq.com](https://console.groq.com) | não |
| OpenRouter | `deepseek/deepseek-r1:free` | [openrouter.ai](https://openrouter.ai/models?max_price=0) | não |
| NVIDIA | `meta/llama-3.3-70b-instruct` | [build.nvidia.com](https://build.nvidia.com) | não |
| Hugging Face | `meta-llama/Llama-3.3-70B-Instruct` | [huggingface.co](https://huggingface.co) | não |
| OpenAI | `gpt-5` *(sem tier grátis)* | [platform.openai.com](https://platform.openai.com) | **sim** |


</Transform>



---
layout: two-cols-header
layoutClass: gap-8
---

# Hands-on


::left::

```python
import os
import asyncio
from dotenv import load_dotenv
from agents import Agent, Runner

async def main():
    load_dotenv()

    agent = Agent(name="", instructions="")

    result = await Runner.run(agent, "")

    print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())
```

::right::


**\#1** Crie um agente de Q&A e use uma API gratuita<br/>

- [ ] escolha um provedor
- [ ] crie a API Key
- [ ] desenvolva o agente

<br/>