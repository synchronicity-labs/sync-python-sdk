# Reference
## Generations
<details><summary><code>client.generations.<a href="src/sync/generations/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync
from sync.common import Audio, GenerationOptions, Video

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generations.create(
    input=[
        Video(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortvid-03a10044-7741-4cfc-816a-5bccd392d1ee.mp4",
        ),
        Audio(
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

<details><summary><code>client.generations.<a href="src/sync/generations/client.py">get</a>(...)</code></summary>
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
client.generations.get(
    id="6533643b-aceb-4c40-967e-d9ba9baac39e",
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

<details><summary><code>client.generations.<a href="src/sync/generations/client.py">list</a>(...)</code></summary>
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
client.generations.list()

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

<details><summary><code>client.generations.<a href="src/sync/generations/client.py">estimate_cost</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from sync import Sync
from sync.common import Audio, GenerationOptions, Video

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generations.estimate_cost(
    input=[
        Video(
            url="https://synchlabs-public.s3.us-west-2.amazonaws.com/david_demo_shortvid-03a10044-7741-4cfc-816a-5bccd392d1ee.mp4",
        ),
        Audio(
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

