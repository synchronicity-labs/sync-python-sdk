# Reference
## Generate
<details><summary><code>client.generate.<a href="src/sync/generate/client.py">generate_controller_create_generation</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import (
    CreateGenerationDtoInputItem_Audio,
    CreateGenerationDtoInputItem_Video,
    Sync,
)

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generate.generate_controller_create_generation(
    model="lipsync-2",
    input=[
        CreateGenerationDtoInputItem_Video(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortvid-03a10044-7741-4cfc-816a-5bccd392d1ee.mp4",
        ),
        CreateGenerationDtoInputItem_Audio(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortaud-27623a4f-edab-4c6a-8383-871b18961a4a.wav",
        ),
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**model:** `CreateGenerationDtoModel` — name of the model to use for generation.
    
</dd>
</dl>

<dl>
<dd>

**input:** `typing.Sequence[CreateGenerationDtoInputItem]` — Array of input objects. Must include one video input and either an audio or text input.
    
</dd>
</dl>

<dl>
<dd>

**options:** `typing.Optional[GenerationOptions]` — additional options available for generation.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — webhook url for generation status updates. once the generation completes we will send a POST request to the webhook url with the generation data.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.generate.<a href="src/sync/generate/client.py">generate_controller_get_generation</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generate.generate_controller_get_generation(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — Job ID
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.generate.<a href="src/sync/generate/client.py">generate_controller_cancel_generation</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generate.generate_controller_cancel_generation(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — Job ID to cancel
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.generate.<a href="src/sync/generate/client.py">generate_controller_get_generations</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generate.generate_controller_get_generations()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `typing.Optional[str]` — Filter generations by status
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Analyze
<details><summary><code>client.analyze.<a href="src/sync/analyze/client.py">analyze_controller_get_cost_estimate</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import (
    CreateGenerationDtoInputItem_Audio,
    CreateGenerationDtoInputItem_Video,
    Sync,
)

client = Sync(
    api_key="YOUR_API_KEY",
)
client.analyze.analyze_controller_get_cost_estimate(
    model="lipsync-2",
    input=[
        CreateGenerationDtoInputItem_Video(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortvid-03a10044-7741-4cfc-816a-5bccd392d1ee.mp4",
        ),
        CreateGenerationDtoInputItem_Audio(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortaud-27623a4f-edab-4c6a-8383-871b18961a4a.wav",
        ),
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**model:** `CreateGenerationDtoModel` — name of the model to use for generation.
    
</dd>
</dl>

<dl>
<dd>

**input:** `typing.Sequence[CreateGenerationDtoInputItem]` — Array of input objects. Must include one video input and either an audio or text input.
    
</dd>
</dl>

<dl>
<dd>

**options:** `typing.Optional[GenerationOptions]` — additional options available for generation.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — webhook url for generation status updates. once the generation completes we will send a POST request to the webhook url with the generation data.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

