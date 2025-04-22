# Reference
## Generate
<details><summary><code>client.generate.<a href="src/sync/generate/client.py">create_generation</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync
from sync.common import GenerationOptions, Input_Audio, Input_Video

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generate.create_generation(
    input=[
        Input_Video(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortvid-03a10044-7741-4cfc-816a-5bccd392d1ee.mp4",
        ),
        Input_Audio(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortaud-27623a4f-edab-4c6a-8383-871b18961a4a.wav",
        ),
    ],
    model="lipsync-2",
    options=GenerationOptions(
        sync_mode="loop",
    ),
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

**model:** `Model` — name of the model to use for generation.
    
</dd>
</dl>

<dl>
<dd>

**input:** `typing.Sequence[Input]` — Array of input objects. Must include one video input item and one audio input item. Audio input items can be provided as either: recorded/captured audio url or a text-to-speech input with tts provider configuration.
    
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

<details><summary><code>client.generate.<a href="src/sync/generate/client.py">get_generation</a>(...)</code></summary>
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
client.generate.get_generation(
    id="6533643b-acbe-4c40-967e-d9ba9baac39e",
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

**id:** `GenerationId` 
    
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

<details><summary><code>client.generate.<a href="src/sync/generate/client.py">list_generations</a>(...)</code></summary>
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
client.generate.list_generations()

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

**status:** `typing.Optional[GenerationStatus]` — Filter generations by status
    
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

<details><summary><code>client.generate.<a href="src/sync/generate/client.py">estimate_cost</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync
from sync.common import GenerationOptions, Input_Audio, Input_Video

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generate.estimate_cost(
    input=[
        Input_Video(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortvid-03a10044-7741-4cfc-816a-5bccd392d1ee.mp4",
        ),
        Input_Audio(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortaud-27623a4f-edab-4c6a-8383-871b18961a4a.wav",
        ),
    ],
    model="lipsync-2",
    options=GenerationOptions(
        sync_mode="loop",
    ),
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

**model:** `Model` — name of the model to use for generation.
    
</dd>
</dl>

<dl>
<dd>

**input:** `typing.Sequence[Input]` — Array of input objects. Must include one video input item and one audio input item. Audio input items can be provided as either: recorded/captured audio url or a text-to-speech input with tts provider configuration.
    
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

