# Reference
## Assets
<details><summary><code>client.assets.<a href="src/sync/assets/client.py">list</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all assets in your organization's media library.
</dd>
</dl>
</dd>
</dl>

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
client.assets.list(
    limit=10,
    sort_by="dateDesc",
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

**project_id:** `typing.Optional[str]` — Filter assets by project ID.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of assets to return (1-100).
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Cursor for pagination.
    
</dd>
</dl>

<dl>
<dd>

**search_query:** `typing.Optional[str]` — Search assets by name.
    
</dd>
</dl>

<dl>
<dd>

**sort_by:** `typing.Optional[AssetSort]` — Sort order for the results.
    
</dd>
</dl>

<dl>
<dd>

**types:** `typing.Optional[typing.Sequence[AssetType]]` — Filter by asset types. Accepts multiple types as a comma-separated list (AUDIO, VIDEO, IMAGE).
    
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

<details><summary><code>client.assets.<a href="src/sync/assets/client.py">get</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific asset by ID.
</dd>
</dl>
</dd>
</dl>

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
client.assets.get(
    id="550e8400-e29b-41d4-a716-446655440000",
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

**id:** `AssetId` 
    
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

## Batch
<details><summary><code>client.batch.<a href="src/sync/batch/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

API for [Batch Processing](/api-reference/guides/batch-processing). Available only for `Scale` and `Enterprise` plans.
</dd>
</dl>
</dd>
</dl>

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
client.batch.create(
    dry_run=True,
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

**input:** `from __future__ import annotations

core.File` — See core.File for more documentation
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — Optional webhook URL to receive batch completion notifications. A POST request will be sent when the batch completes or fails.
    
</dd>
</dl>

<dl>
<dd>

**dry_run:** `typing.Optional[bool]` — When true, validates the input file without processing. Returns validation status without creating generations.
    
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

<details><summary><code>client.batch.<a href="src/sync/batch/client.py">get</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a specific batch, including its current status, processing metrics, and output file URL when available.
</dd>
</dl>
</dd>
</dl>

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
client.batch.get(
    id="batch_abc123",
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

**id:** `BatchId` — The unique identifier of the batch
    
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

<details><summary><code>client.batch.<a href="src/sync/batch/client.py">list</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all batches for your organization with optional filtering by status and creation date. Results are ordered by creation date (newest first).
</dd>
</dl>
</dd>
</dl>

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
client.batch.list()

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

**status:** `typing.Optional[BatchStatus]` — Filter batches by status
    
</dd>
</dl>

<dl>
<dd>

**created_after:** `typing.Optional[dt.datetime]` — Filter batches created after this datetime (ISO 8601 format)
    
</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[dt.datetime]` — Filter batches created before this datetime (ISO 8601 format)
    
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
            url="https://assets.sync.so/docs/example-video.mp4",
        ),
        Audio(
            url="https://assets.sync.so/docs/example-audio.wav",
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

**input:** `typing.Sequence[Input]` — Array of input objects. Must include one video input item and at least one audio input item. Audio input items can be provided as either: recorded/captured audio url or a text-to-speech input with tts provider configuration. When using segments, multiple audio inputs can be provided with unique refId values.
    
</dd>
</dl>

<dl>
<dd>

**options:** `typing.Optional[GenerationOptions]` — additional options available for generation.
    
</dd>
</dl>

<dl>
<dd>

**segments:** `typing.Optional[typing.Sequence[GenerationSegment]]` — segments definition list. When provided, allows defining one or more video segments with different audio inputs for each segment. Each segment specifies a time range and references an audio input by refId.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — webhook url for generation status updates. once the generation completes we will send a POST request to the webhook url with the generation data.
    
</dd>
</dl>

<dl>
<dd>

**output_file_name:** `typing.Optional[str]` — Base filename for the generated output without extension. The .mp4 extension will be added automatically.  Only alphanumeric characters, underscores, and hyphens are allowed, up to 255 characters.
    
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

<details><summary><code>client.generations.<a href="src/sync/generations/client.py">create_with_files</a>(...)</code></summary>
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
client.generations.create_with_files(
    model="lipsync-2",
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

**model:** `Model` 
    
</dd>
</dl>

<dl>
<dd>

**video:** `from __future__ import annotations

typing.Optional[core.File]` — See core.File for more documentation
    
</dd>
</dl>

<dl>
<dd>

**audio:** `from __future__ import annotations

typing.Optional[core.File]` — See core.File for more documentation
    
</dd>
</dl>

<dl>
<dd>

**input:** `typing.Optional[typing.List[Input]]` — Array of input objects. Can be used to provide urls for larger files. Each input should either have a file or a url. Audio input items can be provided as either: recorded/captured audio url or a text-to-speech input with tts provider configuration.
    
</dd>
</dl>

<dl>
<dd>

**options:** `typing.Optional[GenerationOptions]` 
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` 
    
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

**status:** `typing.Optional[typing.Sequence[GenerationStatus]]` — Filter generations by status. Accepts multiple statuses as a comma-separated list.
    
</dd>
</dl>

<dl>
<dd>

**ids:** `typing.Optional[typing.Sequence[str]]` — Filter generations by ID. Accepts multiple IDs as a comma-separated list.
    
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
            url="https://assets.sync.so/docs/example-video.mp4",
        ),
        Audio(
            url="https://assets.sync.so/docs/example-audio.wav",
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

**input:** `typing.Sequence[Input]` — Array of input objects. Must include one video input item and at least one audio input item. Audio input items can be provided as either: recorded/captured audio url or a text-to-speech input with tts provider configuration. When using segments, multiple audio inputs can be provided with unique refId values.
    
</dd>
</dl>

<dl>
<dd>

**options:** `typing.Optional[GenerationOptions]` — additional options available for generation.
    
</dd>
</dl>

<dl>
<dd>

**segments:** `typing.Optional[typing.Sequence[GenerationSegment]]` — segments definition list. When provided, allows defining one or more video segments with different audio inputs for each segment. Each segment specifies a time range and references an audio input by refId.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — webhook url for generation status updates. once the generation completes we will send a POST request to the webhook url with the generation data.
    
</dd>
</dl>

<dl>
<dd>

**output_file_name:** `typing.Optional[str]` — Base filename for the generated output without extension. The .mp4 extension will be added automatically.  Only alphanumeric characters, underscores, and hyphens are allowed, up to 255 characters.
    
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

## Models
<details><summary><code>client.models.<a href="src/sync/models/client.py">list</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all available models for the authenticated user. Returns active (non-deprecated) models the user has access to, including any feature-flagged models enabled for their account.
</dd>
</dl>
</dd>
</dl>

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
client.models.list()

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

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

