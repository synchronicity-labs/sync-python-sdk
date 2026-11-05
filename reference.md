# Reference
## Account
<details><summary><code>client.account.<a href="src/sync/account/client.py">get</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the account, plan, limits and balance behind these credentials. Call it before submitting work to check plan limits and remaining credits or free allowance, and after a 402, 403 or 429 to decide how to recover: `billingModel` says whether to top up credits (`credits`), pay or update the payment method (`usage`), upgrade (`free`) or contact sync. (`enterprise`). Send people to `billingUrl` for anything that needs a payment.
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
client.account.get()

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

<details><summary><code>client.assets.<a href="src/sync/assets/client.py">create_upload</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Request a presigned URL to upload a local file. PUT the file bytes to the returned uploadUrl with the same Content-Type, then register the file as an asset via POST /v2/assets using the returned url. Single uploads are capped at 5GB.
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
client.assets.create_upload(
    file_name="my-video.mp4",
    content_type="video/mp4",
    size=10485760,
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

**file_name:** `str` — The name of the file to upload.
    
</dd>
</dl>

<dl>
<dd>

**content_type:** `str` — The MIME content type of the file (e.g. video/mp4).
    
</dd>
</dl>

<dl>
<dd>

**size:** `int` — The size of the file in bytes. Single uploads are capped at 5GB.
    
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

<details><summary><code>client.assets.<a href="src/sync/assets/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Register a media URL as a reusable asset and get back its id. Use the id in generation inputs (input[].assetId) or as a voice clone sample. To upload a local file, first request a presigned URL via POST /v2/assets/upload, PUT the file there, then register the returned url here. Registration verifies the upload happened and enforces plan limits on the actual file size.

projectId is optional. When provided it must reference a project in your organization — a stale or foreign id is rejected with a 422 and errorCode project_not_found; omit the field if you don't need the asset attached to a project.
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
client.assets.create(
    url="https://assets.sync.so/org-123/my-video.mp4",
    type="VIDEO",
    name="my-video.mp4",
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

**url:** `str` — The public URL of the media to register — e.g. the url returned by POST /v2/assets/upload. Registration verifies the upload happened and enforces plan limits on the actual file size.
    
</dd>
</dl>

<dl>
<dd>

**type:** `AssetType` — The type of asset.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — An optional display name for the asset.
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `typing.Optional[AssetVisibility]` — Who can see the asset. Defaults to USER.
    
</dd>
</dl>

<dl>
<dd>

**project_id:** `typing.Optional[ProjectId]` — Optionally attach the asset to a project (created via POST /v2/projects) so it appears in Studio under that project's media. Must reference a project in your organization — otherwise the request is rejected with 422.
    
</dd>
</dl>

<dl>
<dd>

**input_type:** `typing.Optional[AssetInputType]` — The source of the asset.
    
</dd>
</dl>

<dl>
<dd>

**thumbnail_url:** `typing.Optional[str]` — Optional thumbnail URL for the asset.
    
</dd>
</dl>

<dl>
<dd>

**size:** `typing.Optional[int]` — File size in bytes.
    
</dd>
</dl>

<dl>
<dd>

**format:** `typing.Optional[str]` — File format or extension.
    
</dd>
</dl>

<dl>
<dd>

**duration_seconds:** `typing.Optional[float]` — Media duration in seconds.
    
</dd>
</dl>

<dl>
<dd>

**width:** `typing.Optional[int]` — Width in pixels for video or image assets.
    
</dd>
</dl>

<dl>
<dd>

**height:** `typing.Optional[int]` — Height in pixels for video or image assets.
    
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

<details><summary><code>client.assets.<a href="src/sync/assets/client.py">update</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an asset's name or visibility. With API-key auth the asset must be owned by the key owner; organization-shared assets can only be updated from an admin/owner session. An asset you can view but not edit returns a 403 with errorCode asset_forbidden; an unknown id returns a 404 with errorCode asset_not_found.
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
client.assets.update(
    id="550e8400-e29b-41d4-a716-446655440000",
    name="Renamed asset",
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

**name:** `typing.Optional[str]` — A new display name for the asset.
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `typing.Optional[AssetVisibility]` — Update who can see the asset.
    
</dd>
</dl>

<dl>
<dd>

**duration_seconds:** `typing.Optional[float]` — Updated media duration in seconds.
    
</dd>
</dl>

<dl>
<dd>

**size:** `typing.Optional[int]` — Updated file size in bytes.
    
</dd>
</dl>

<dl>
<dd>

**format:** `typing.Optional[str]` — Updated file format or extension.
    
</dd>
</dl>

<dl>
<dd>

**width:** `typing.Optional[int]` — Updated width in pixels.
    
</dd>
</dl>

<dl>
<dd>

**height:** `typing.Optional[int]` — Updated height in pixels.
    
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

<details><summary><code>client.assets.<a href="src/sync/assets/client.py">delete</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete an asset. With API-key auth the asset must be owned by the key owner; organization-shared assets can only be deleted from an admin/owner session. An asset you can view but not delete returns a 403 with errorCode asset_forbidden; an unknown id returns a 404 with errorCode asset_not_found.
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
client.assets.delete(
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

Create a batch processing job from a JSONL file. Requires a paid plan; free accounts get 402 `plan_feature_unavailable`. Send the file in multipart field `input` (or the accepted `file` alias); it must be 5 MB or smaller. On Scale and above a batch holds 20-500 records by default and is queued, holding one concurrency slot. Below Scale every record runs as a generation right away, so a batch holds 1 record up to your plan's concurrency limit: more records than that returns 400, and more records than your currently free generation slots returns 429 `concurrency_limit_reached`. Credit-billed plans reserve credits for the whole batch at submit and get 402 `insufficient_credits` when the balance is short. Each line must contain `request_id`, endpoint exactly `/v2/generate`, and a generation `payload`. To send the records as a JSON array instead of a file, use "Create Batch from Rows", the `application/json` form of the same endpoint. Errors name a refused record by its 1-based line, counting non-empty lines: dialogue edit refusals return it as `lineNumber`, other record errors only in `message`.
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

**webhook_url:** `typing.Optional[str]` — Optional webhook URL to receive batch completion notifications. A POST request will be sent when the batch completes or fails, with a Sync-Signature header (`t=<unix>,v1=<hmac_sha256>`) signed with the organization webhook secret and a stable Sync-Delivery-Id header. Delivery is attempted up to six times over about two hours.
    
</dd>
</dl>

<dl>
<dd>

**dry_run:** `typing.Optional[bool]` — When true, validates the JSONL file and returns `{ "status": "VALIDATED" }` without creating a batch.
    
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

<details><summary><code>client.batch.<a href="src/sync/batch/client.py">create_from_rows</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The `application/json` form of `POST /v2/batch`, the same endpoint as "Create Batch": send the records in a `rows` array instead of a JSONL file. Each row is the same object as one JSONL line and is validated the same way: 20-500 rows by default on Scale and above, 1 row up to your free generation slots below Scale, 5 MB or smaller when serialized as JSONL, unique `request_id` values, and endpoint exactly `/v2/generate`. Errors name a refused row by its line, where line N is `rows[N-1]`: dialogue edit refusals return it as `lineNumber`, other record errors only in `message`. Requires a paid plan. In early access, enabled per organization, a row's payload can carry `dialogueEdit` to render a completed preview from POST /v2/dialogue-edits: send one video input, the video the preview was made from, and no audio input. All dialogue edit rows in a batch must come from the same source video. Each row is expanded at submit into the request POST /v2/generate builds for that preview and is charged the same. A dialogue edit row that cannot be rendered refuses the whole batch with the `/v2/generate` errorCode (for example dialogue_edit_not_found, 422) and `lineNumber`. See [Batch Processing](/api-reference/guides/batch-processing).
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
from sync.common import (
    BatchRow,
    CreateGenerationDto,
    DialogueEditReference,
    Video,
)

client = Sync(
    api_key="YOUR_API_KEY",
)
client.batch.create_from_rows(
    rows=[
        BatchRow(
            request_id="line-2",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="fa350e8a-0c6b-50c3-96de-7e4ce81ed0ce",
                ),
            ),
        ),
        BatchRow(
            request_id="line-3",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="ddaea593-cf1f-5916-aaef-c60ab5f63090",
                ),
            ),
        ),
        BatchRow(
            request_id="line-4",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="532a08cd-becc-5630-8109-58d22206db7e",
                ),
            ),
        ),
        BatchRow(
            request_id="line-5",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="68f897e5-78e3-55d3-9ca3-d8ba0d16c5c4",
                ),
            ),
        ),
        BatchRow(
            request_id="line-6",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="f4aa2ca8-006d-5301-baf7-4ce543188328",
                ),
            ),
        ),
        BatchRow(
            request_id="line-7",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="636f1dd4-f4e1-508d-8cdd-6dac1dd002a3",
                ),
            ),
        ),
        BatchRow(
            request_id="line-8",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="8f6640f5-6139-5271-ab33-f43fc91fc1ad",
                ),
            ),
        ),
        BatchRow(
            request_id="line-9",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="6c101a02-cdd8-5ec0-9df9-1ffea33a11bd",
                ),
            ),
        ),
        BatchRow(
            request_id="line-10",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="258f60c2-b635-5ab6-a565-ae81a709e221",
                ),
            ),
        ),
        BatchRow(
            request_id="line-11",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="09dc425b-4d7e-5813-8c6c-81bd38993a7b",
                ),
            ),
        ),
        BatchRow(
            request_id="line-12",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="b93c54d3-28d6-5fa3-abaf-5220c38e31a1",
                ),
            ),
        ),
        BatchRow(
            request_id="line-13",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="e8a1dea0-b3f9-5266-badd-f8a2aae77ea3",
                ),
            ),
        ),
        BatchRow(
            request_id="line-14",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="a09967c4-8171-582f-8dba-1ba07d55f918",
                ),
            ),
        ),
        BatchRow(
            request_id="line-15",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="39df4e4f-b23d-54ca-99a8-f29ec567790b",
                ),
            ),
        ),
        BatchRow(
            request_id="line-16",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="0370783a-12d5-5dfb-8736-49118428df47",
                ),
            ),
        ),
        BatchRow(
            request_id="line-17",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="a65eecc2-ad79-5123-acf7-e81a57b2422f",
                ),
            ),
        ),
        BatchRow(
            request_id="line-18",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="a0200ef6-d140-50bb-9784-3b9e265be374",
                ),
            ),
        ),
        BatchRow(
            request_id="line-19",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="06cc754a-b625-58c2-ad2d-74ec08fb517a",
                ),
            ),
        ),
        BatchRow(
            request_id="line-20",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="32889341-cc9e-59c6-b18a-32bbb525c26e",
                ),
            ),
        ),
        BatchRow(
            request_id="line-21",
            payload=CreateGenerationDto(
                model="sync-3",
                input=[
                    Video(
                        url="https://assets.sync.so/docs/example-video.mp4",
                    )
                ],
                dialogue_edit=DialogueEditReference(
                    id="f6568dbc-0390-5227-b107-64c3842adb3b",
                ),
            ),
        ),
    ],
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

**rows:** `typing.Sequence[BatchRow]` — The batch records: 20-500 by default on Scale and above, 1 up to your free generation slots below Scale. Each row contains `request_id`, endpoint exactly `/v2/generate`, and a generation `payload`, as on a JSONL line.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — Optional webhook URL to receive batch completion notifications. A POST request will be sent when the batch completes or fails, with a Sync-Signature header (`t=<unix>,v1=<hmac_sha256>`) signed with the organization webhook secret and a stable Sync-Delivery-Id header. Delivery is attempted up to six times over about two hours.
    
</dd>
</dl>

<dl>
<dd>

**dry_run:** `typing.Optional[bool]` — When true, validates the rows, including dialogue edit expansion, and returns `{ "status": "VALIDATED" }` without creating a batch.
    
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

## DialogueEdits
<details><summary><code>client.dialogue_edits.<a href="src/sync/dialogue_edits/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies word-level edits to a transcript from `POST /v2/transcriptions` and synthesizes preview audio for the same window: only the edited spans are re-spoken in a voice cloned from the source, everything else stays the original recording. Poll `GET /v2/dialogue-edits/{id}` until `status` is `COMPLETED`, `COMPLETED_PARTIAL` or `FAILED`; a completed or partially completed job carries `previewAudioUrl`, the retimed `resultTranscript` and the edited regions as `resultSlots`. Edits that cannot be applied to the transcript are refused with a 400 before a job exists. An API-key request is admitted only for the whole video (leave startMs and endMs unset) and only when the organization's rollout enables segment lipsync and section expansion: a partial window is refused with errorCode `dialogue_edit_unsupported` (422), a rollout without both flags with `dialogue_edit_retime_required` (422), and a rollout that cannot be evaluated with `generation_infra_service_unavailable` (503; retry with backoff). Studio sessions may select a window. Normal billing, planning, duration and rate limits still apply.
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
from sync.common import (
    DialogueEditOperation_Change,
    Transcript,
    TranscriptSegment,
    TranscriptWord,
)

client = Sync(
    api_key="YOUR_API_KEY",
)
client.dialogue_edits.create(
    source_video_url="https://assets.sync.so/docs/example-video.mp4",
    transcript=Transcript(
        segments=[
            TranscriptSegment(
                id="seg_1",
                words=[
                    TranscriptWord(
                        id="w_1",
                        text="The",
                        start_ms=120,
                        end_ms=260,
                    ),
                    TranscriptWord(
                        id="w_2",
                        text="quarterly",
                        start_ms=260,
                        end_ms=820,
                    ),
                    TranscriptWord(
                        id="w_3",
                        text="results",
                        start_ms=820,
                        end_ms=1240,
                    ),
                ],
            )
        ],
        speaker_count=1,
    ),
    edits=[
        DialogueEditOperation_Change(
            word_id="w_2",
            replacement="annual",
        )
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

**transcript:** `Transcript` — The transcript the edits refer to, as returned by GET /v2/transcriptions/{id}. Edits name words by their id in this transcript. Word timings are in milliseconds from the start of the source video.
    
</dd>
</dl>

<dl>
<dd>

**edits:** `typing.Sequence[DialogueEditOperation]` — The edits to apply: change replaces one word (wordId, replacement), remove cuts a contiguous run of words (wordIds). Between 1 and 100 edits per job.
    
</dd>
</dl>

<dl>
<dd>

**source_video_url:** `str` — URL of the source video the transcript was made from, hosted in sync. storage (upload it via POST /v2/assets/upload first).
    
</dd>
</dl>

<dl>
<dd>

**start_ms:** `typing.Optional[int]` — Start of the edited window, in milliseconds from the start of the source. Use the same window the transcript was made for. Defaults to 0. An API-key request must leave startMs and endMs unset; the edit then covers the whole video.
    
</dd>
</dl>

<dl>
<dd>

**end_ms:** `typing.Optional[int]` — End of the edited window, in milliseconds from the start of the source. Omit to run to the end. The window cannot exceed 10 minutes. An API-key request must leave startMs and endMs unset to edit the whole video.
    
</dd>
</dl>

<dl>
<dd>

**voice_id:** `typing.Optional[str]` — Opaque voice id returned as voiceId by an earlier dialogue-edit job of the same source. Reusing it skips cloning the voice again. Omit on the first job for a source. Ids your organization has not used before are ignored.
    
</dd>
</dl>

<dl>
<dd>

**project_id:** `typing.Optional[ProjectId]` — Optional id of a project in your organization to file the job under.
    
</dd>
</dl>

<dl>
<dd>

**rerun_of_job_id:** `typing.Optional[DialogueEditJobId]` — Id of the completed dialogue-edit job this request revises, when regenerating a preview after adjusting the edits. Informational lineage only; unknown ids are ignored.
    
</dd>
</dl>

<dl>
<dd>

**transcription_job_id:** `typing.Optional[TranscriptionJobId]` — The completed transcription job this edit is based on. Send it so the edit and the transcript agree on the source: the request is refused when that job's source, window or words do not match this edit.
    
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

<details><summary><code>client.dialogue_edits.<a href="src/sync/dialogue_edits/client.py">get</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the job status and, once it completed, the preview audio url, the retimed transcript and the edited regions. `COMPLETED`, `COMPLETED_PARTIAL` and `FAILED` are terminal; `error.code` says why a job failed.
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
client.dialogue_edits.get(
    id="7644754c-bdfc-4d51-a78f-e0cb0cbbd40f",
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

**id:** `DialogueEditJobId` — Dialogue edit job id.
    
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

## Errors
<details><summary><code>client.errors.<a href="src/sync/errors/client.py">list</a>()</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the full catalog of machine-readable error codes — each with a human-readable message and a suggested fix. It covers generation failures plus the coded errors returned by the assets, voices, and TTS endpoints (e.g. project_not_found, voice_not_found, asset_forbidden). This endpoint is unauthenticated. Pair it with the errorCode field returned on a failed generation or on a coded 4xx/5xx response so an agent can look up what went wrong and how to correct it without hard-coding error strings.
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
client.errors.list()

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

## Feedback
<details><summary><code>client.feedback.<a href="src/sync/feedback/client.py">submit</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Report a problem you hit with the API or the sync. MCP server, such as an error that didn't say what to fix, a wrong result, a missing capability, or a workaround you needed. Send one report per problem. The sync. team reviews reports daily. Works with an API key, an OAuth access token, or a Studio session. Submitting feedback doesn't change, retry, or cancel any job. Limited to 30 reports per minute per caller. Unknown body fields return 400.
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
import uuid

from sync import Sync

client = Sync(
    api_key="YOUR_API_KEY",
)
client.feedback.submit(
    kind="confusing_error",
    severity="major",
    message="POST /v2/generate returned generation_input_video_inaccessible for a presigned URL that plays in a browser. Saying whether the URL had expired or was blocked would have helped.",
    tool="generations.create",
    error_code="generation_input_video_inaccessible",
    generation_id=uuid.UUID(
        "6533643b-acbb-4c4f-a5b3-5ba2e5ab6b5f",
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

**kind:** `FeedbackKind` — The kind of problem: `confusing_error` (an error that didn't say what to fix), `bug` (a wrong result or crash), `missing_capability` (an endpoint, tool, or option you needed), `workaround` (extra steps you had to take), `docs` (documentation or a description that misled you), or `other`.
    
</dd>
</dl>

<dl>
<dd>

**message:** `str` — What you tried, what happened, and what would have helped. Include the exact error text. Don't include personal data or secrets. 1 to 4,000 characters.
    
</dd>
</dl>

<dl>
<dd>

**severity:** `typing.Optional[FeedbackSeverity]` — `blocker`: you couldn't finish. `major`: you finished with a workaround. `minor`: an annoyance.
    
</dd>
</dl>

<dl>
<dd>

**tool:** `typing.Optional[str]` — The MCP tool or API operation the feedback is about.
    
</dd>
</dl>

<dl>
<dd>

**error_code:** `typing.Optional[str]` — The error code you received, such as an `errorCode` field.
    
</dd>
</dl>

<dl>
<dd>

**generation_id:** `typing.Optional[uuid.UUID]` — The generation the feedback is about.
    
</dd>
</dl>

<dl>
<dd>

**job_id:** `typing.Optional[str]` — Another job the feedback is about, such as an import, transcription, or translation ID.
    
</dd>
</dl>

<dl>
<dd>

**source:** `typing.Optional[FeedbackSource]` — Where the report comes from. Defaults to `api`. The sync. MCP server sends `mcp`.
    
</dd>
</dl>

<dl>
<dd>

**mcp_version:** `typing.Optional[str]` — The sync. MCP server version. Sent by the MCP server.
    
</dd>
</dl>

<dl>
<dd>

**client:** `typing.Optional[FeedbackClient]` — The client or agent sending the report.
    
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

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a lip sync generation with `application/json` — provide each input by `url` or by `assetId` from an uploaded asset. For reusable or large local files, upload them first with POST /v2/assets/upload and pass the returned `assetId`; see [Asset Uploads](/developer-guides/asset-uploads). Use the multipart "Create Generation with Files" form only when uploading direct audio, video, or image file fields; it has a 5 GiB per-file application parser limit, subject to your plan and any lower proxy limits. Nested fields such as input, options, segments, outputAudio, dubParams, and dialogueEdit must be JSON strings in multipart requests. If a `text` input requires speech synthesis and the ElevenLabs provider is temporarily unavailable, the request returns errorCode elevenlabs_service_unavailable: 504 for provider timeouts and 503 for other provider outages for unkeyed requests. Keyed uncertain outcomes return 503 IDEMPOTENCY_OUTCOME_UNKNOWN instead. An API-key request that passes dialogueEdit is refused with errorCode dialogue_edit_retime_required (422) when the organization's rollout lacks segment lipsync and section expansion. A dialogueEdit that removes more speech than the surrounding footage can absorb returns errorCode dialogue_edit_removal_too_large (422). When the failing section can be identified, `dialogueEditSection` on the error names it; change it and create a new preview before submitting again. Retrying the same preview fails again. Send the optional Idempotency-Key header on the first request and reuse it with the same payload on retries. An accepted replay returns 200 with the original generation's current state and Idempotency-Replayed: true. A retry after that generation ended FAILED or REJECTED starts a new generation instead (201). An API-key request without the header that is identical to one your organization sent in the last 60 seconds returns 409 DUPLICATE_SUBMISSION with the original generationId; send a unique Idempotency-Key with each generation you intend. See [Idempotent Requests](/api-reference/guides/idempotency) for key validation, conflicts, retention, duplicates, and uncertain-outcome recovery.
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
from sync.common import DubDto, Video

client = Sync(
    api_key="YOUR_API_KEY",
)
client.generations.create(
    input=[
        Video(
            url="https://assets.sync.so/docs/example-video.mp4",
        )
    ],
    model="lipsync-2",
    dub_params=DubDto(
        provider_name="elevenlabs",
        target_lang="es",
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

**input:** `typing.Sequence[Input]` — Normal lipsync requests must include exactly one visual input (video or image) and one audio or text input. Dubbed lipsync requests using dubParams must include exactly one video input and no audio or text input, because Sync extracts the dubbing source audio from that video. Image inputs are only supported with the sync-3 model. When using segments, audio or text inputs can carry unique refId values.
    
</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `typing.Optional[str]` — Case-sensitive organization-scoped key, 1–128 characters matching [A-Za-z0-9._~-]+. Send exactly one header. Reuse the same key and payload for retries of one action; a retry after the generation ended FAILED or REJECTED starts a new one. Use a unique key per intended generation. Retained seven days from acceptance, longer while active or unresolved. Not a JSON field.
    
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

**output_audio:** `typing.Optional[OutputAudio]` — One audio input that plays over the whole finished output from its first second, replacing the sound of every part, lipsynced or not. Use it with segments, for example one dubbed track for a whole video where some segments set lipsync to false. When any segment sets lipsync to false and this is omitted, the only audio input is used. Not available with a custom output bucket, zero data retention or a retention override.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — Webhook URL for generation status updates. When the generation reaches a terminal state, Sync sends a POST request with the generation payload and a Sync-Signature header. Verify the header with the organization webhook secret from GET /v2/organizations/webhook/secret. HTTPS is strongly recommended.
    
</dd>
</dl>

<dl>
<dd>

**output_file_name:** `typing.Optional[str]` — Base filename for the generated output without extension. The .mp4 extension will be added automatically. Only alphanumeric characters, underscores, and hyphens are allowed, up to 255 characters.
    
</dd>
</dl>

<dl>
<dd>

**dub_params:** `typing.Optional[DubDto]` — Dubbing parameters. When present, audio is extracted from the single video input, dubbed via ElevenLabs into the target language, and then lipsync is run with the dubbed audio. Do not include audio or text inputs with dubParams; requests that send both are rejected.
    
</dd>
</dl>

<dl>
<dd>

**project_id:** `typing.Optional[ProjectId]` — Optionally attach this generation to a project (created via POST /v2/projects) so it appears in Studio under that project. Must reference a project in your organization — otherwise the request is rejected with 422.
    
</dd>
</dl>

<dl>
<dd>

**dialogue_edit:** `typing.Optional[DialogueEditReference]` — Use the id of a completed dialogue edit from POST /v2/dialogue-edits to supply the audio and edited regions. Requires a preview that ran segment lipsync and section expansion (see the job's segmentLipsyncEnabled and sectionExpansionEnabled). Send exactly one video input, the same video the dialogue edit was made from, and no audio input, segments or dubParams. Billing, status, wait and webhooks work as for any generation.
    
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

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The multipart/form-data form of `POST /v2/generate` — the same endpoint as "Create Generation", for uploading local files directly instead of passing URLs. Send each file under a field named for its type (`video`, `image`, `audio`), at most one of each. The application parser allows up to 5 GiB (5 × 1024³ bytes) per file, 3 files, 32 fields, 35 total parts, and 1 MiB per field. A file over the parser limit returns 413 generation_input_validation_failed, and a file over your plan limit returns 422 file_size_exceeds_plan_limit. Proxy limits may be lower; this ceiling does not guarantee a 5 GiB direct transfer. Each file is saved as an asset in your organization and passed to the generation by `assetId`. For large files, upload via POST /v2/assets/upload first and pass the `assetId`, so retries don't resend the file. Nested fields such as `input`, `options`, `segments`, `outputAudio`, `dubParams`, and `dialogueEdit` must be sent as JSON strings in multipart requests. Image inputs are sync-3 only. If a `text` input requires speech synthesis and the ElevenLabs provider is temporarily unavailable, the request returns errorCode elevenlabs_service_unavailable: 504 for provider timeouts and 503 for other provider outages for unkeyed requests. Keyed uncertain outcomes return 503 IDEMPOTENCY_OUTCOME_UNKNOWN instead. An API-key request that passes dialogueEdit is refused with errorCode dialogue_edit_retime_required (422) when the organization's rollout lacks segment lipsync and section expansion. A dialogueEdit that removes more speech than the surrounding footage can absorb returns errorCode dialogue_edit_removal_too_large (422). When the failing section can be identified, `dialogueEditSection` on the error names it; change it and create a new preview before submitting again. Retrying the same preview fails again. Send the optional Idempotency-Key header on the first request and reuse it with the same payload on retries. An accepted replay returns 200 with the original generation's current state and Idempotency-Replayed: true. A retry after that generation ended FAILED or REJECTED starts a new generation instead (201). An API-key request without the header that is identical to one your organization sent in the last 60 seconds returns 409 DUPLICATE_SUBMISSION with the original generationId; send a unique Idempotency-Key with each generation you intend. See [Idempotent Requests](/api-reference/guides/idempotency) for key validation, conflicts, retention, duplicates, and uncertain-outcome recovery.
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

**image:** `from __future__ import annotations

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

**input:** `typing.Optional[typing.List[Input]]` — Array of input objects, encoded as a JSON string in multipart requests. Can be used to provide URLs or assetIds for larger files. Each input should either have a file, a url, or an assetId. Audio input items can be provided as either recorded/captured audio URL or a text-to-speech input with TTS provider configuration.
    
</dd>
</dl>

<dl>
<dd>

**options:** `typing.Optional[GenerationOptions]` — Optional generation options, encoded as a JSON string in multipart requests.
    
</dd>
</dl>

<dl>
<dd>

**segments:** `typing.Optional[typing.List[GenerationSegment]]` — Optional segment definitions, encoded as a JSON string in multipart requests.
    
</dd>
</dl>

<dl>
<dd>

**output_audio:** `typing.Optional[OutputAudio]` — Optional audio input that plays over the whole finished output, encoded as a JSON string in multipart requests, for example `{"refId":"dub"}`. Use with segments. The refId must name an audio input sent by url or assetId: an uploaded audio file has no refId.
    
</dd>
</dl>

<dl>
<dd>

**dub_params:** `typing.Optional[DubDto]` — Optional dubbing parameters, encoded as a JSON string in multipart requests.
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**output_file_name:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**project_id:** `typing.Optional[ProjectId]` — Optional project id to attach the generation to.
    
</dd>
</dl>

<dl>
<dd>

**dialogue_edit:** `typing.Optional[DialogueEditReference]` — Optional reference to a completed dialogue edit (its id from POST /v2/dialogue-edits) to render its preview into a video, encoded as a JSON string in multipart requests. Send one video input from the same source and no audio, segments or dubParams.
    
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

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve the current generation state. This /v2/generate/{id} route supports the wait, timeout and include options below.
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

**wait:** `typing.Optional[bool]` — When true, long-poll: hold the request open until the generation reaches a terminal status (COMPLETED/FAILED/REJECTED) or the timeout elapses, then return the latest state. Waits are short (10s max) — treat this as a convenience for jobs about to finish, and poll again (the response includes a `Retry-After: 2` header) or use a webhook for longer jobs. wait=true responses also carry `X-Sync-Wait-Mode: long_poll` and `X-Sync-Wait-Timeout-Seconds` headers. Cannot be combined with include=progress.
    
</dd>
</dl>

<dl>
<dd>

**timeout:** `typing.Optional[float]` — Max seconds to hold a wait=true request open (default 5, max 10 — values outside 1-10 are rejected with a 400). On timeout the current (non-terminal) generation is returned with HTTP 200, so check `status` and poll again, or use a webhook for long jobs.
    
</dd>
</dl>

<dl>
<dd>

**include:** `typing.Optional[str]` — Comma-separated extra fields to include. include=progress adds a progress_percent field (fetched live from the inference service).
    
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

<details><summary><code>client.generations.<a href="src/sync/generations/client.py">download</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Obtain the available full output of a completed generation in your
organization. Authenticate with `x-api-key`; no Studio project or user
session is required. Any valid API key belonging to the generation's
organization can request the URL.

The successful response is an **unquoted URL in a text/plain body**,
not JSON, a redirect, or the video itself. Fetch that URL separately
without forwarding your API key.

```bash
download_url=$(curl --fail-with-body --silent --show-error \
  -H "x-api-key: $SYNC_API_KEY" \
  "https://api.sync.so/v2/generations/$GENERATION_ID/download") &&
curl --fail --location "$download_url" --output output.mov
```

The URL resolves an existing output using your organization's current
plan and billing-version eligibility. Free and watermark-required plans
receive the watermarked derivative when present. Entitled plans (such
as v2 Creator and v3 Starter or higher) receive the clean output when
available. Historical outputs can have the watermark burned in, so an
upgrade does not guarantee every old output becomes watermark-free.
Outputs created without a watermark can remain clean after a downgrade.
If no watermarked derivative exists, the resolver retains its existing
fallback to the original output; changing plans does not rewrite files.
This endpoint does not generate a new render or remove burned-in watermarks.

Signed S3 URLs request seven-day validity, but credential expiry,
revocation, access changes, or file deletion can make them unusable
sooner. Request this endpoint again for a fresh signed URL while the
output is still available. The selected S3 file is checked before
signing; a successful response does not guarantee future availability.
Older URL-only records return their stored URL unchanged, without
checking its availability or extending its original expiration.
These URLs are download credentials: keep them private.

Errors use the standard JSON error body and stable `errorCode`:

| Status | Code | Meaning / next step |
| --- | --- | --- |
| 400 | — | Invalid generation UUID. |
| 401 | — | API key missing, invalid, or revoked. |
| 404 | `generation_not_found` | Missing, deleted, or outside your organization. |
| 404 | `generation_output_unavailable` | No eligible output reference or the selected file is missing; contact support. |
| 409 | `generation_not_ready` | Pending or processing; poll Get Generation until COMPLETED. |
| 422 | `generation_not_downloadable` | Failed or rejected; inspect the generation error. |
| 503 | `generation_download_unavailable` | Storage lookup or signing failed; retry with backoff. |

Authentication also returns 422 for draft organizations. Requesting a
download URL does not create a project, incur a generation charge, or
restore deleted files.
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
client.generations.download(
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

**id:** `GenerationId` 
    
</dd>
</dl>

<dl>
<dd>

**file_name:** `typing.Optional[str]` — Optional download filename. Its extension is replaced with the output's format. Ignored for URL-only outputs.
    
</dd>
</dl>

<dl>
<dd>

**x_sync_accelerate:** `typing.Optional[str]` — Send true to request transfer acceleration; falls back to the standard endpoint when acceleration is disabled.
    
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

**source:** `typing.Optional[typing.Sequence[str]]` — Filter generations by source. Accepts multiple sources as a comma-separated list.
    
</dd>
</dl>

<dl>
<dd>

**project_id:** `typing.Optional[ProjectId]` — Return only generations in this project. Must be a UUID. A project you can't access returns an empty list.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of generations to return (1-100). When set, results are ordered newest first and can be paged with `cursor`.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — ID of the last generation on the previous page. Requires `limit`.
    
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

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Estimate a generation from its model and billable duration in seconds. Supply a finite positive duration and, optionally, a finite positive fps (defaults to 25 for credit-billed organizations and 30 otherwise). Set `workflow` to `translate-and-dub` to include dubbing; the response then carries a `breakdown`. `durationCheck` says whether your account and the model allow the quoted duration. No media is fetched and no generation is created. POST /v2/generate/estimate-cost is an alias of this endpoint. Invalid request fields return 400. If the billing calculation rejects the duration or frame rate, it returns 422 cost_estimate_unavailable without price fields.
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
client.generations.estimate_cost(
    model="model",
    duration=1.1,
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

**model:** `str` — Model to estimate, for example lipsync-2 or sync-3.
    
</dd>
</dl>

<dl>
<dd>

**duration:** `float` — Finite, positive billable duration in seconds.
    
</dd>
</dl>

<dl>
<dd>

**fps:** `typing.Optional[float]` — Source video frame rate. When omitted, credit-billed organizations are quoted at 25, the rate generation admission holds credits at when the source frame rate cannot be read; other organizations at 30.
    
</dd>
</dl>

<dl>
<dd>

**workflow:** `typing.Optional[EstimateWorkflow]` — Omit for lip-sync only. `translate-and-dub` includes dubbing and lip-sync, estimated using the source duration. Actual output duration may differ.
    
</dd>
</dl>

<dl>
<dd>

**reasoning_enabled:** `typing.Optional[bool]` — Include reasoning pricing when supported by the model.
    
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

<details><summary><code>client.generations.<a href="src/sync/generations/client.py">delete</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a generation. Generations are organization-scoped, so any member — or an API key for the organization — can delete one. Only generations in a terminal state can be deleted; deleting one that is still processing returns 409 (errorCode `generation_not_deletable_while_processing`). Returns the deleted generation in its stored shape (`modelName`, `inputs`, `outputMediaUrl`, `deletedAt`), not the Get Generation shape.
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
client.generations.delete(
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

## Organizations
<details><summary><code>client.organizations.<a href="src/sync/organizations/client.py">get_webhook_secret</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve your organization's webhook signing secret. This is a public, authenticated endpoint you can use to verify the `Sync-Signature` header on generation and batch webhook deliveries: Sync signs the raw JSON request body as HMAC-SHA256 over `${timestamp}.${rawBody}` and sends it as `Sync-Signature: t=<unix>,v1=<hmac_sha256>`. Store the full `whsec_...` value securely. `masked=true` returns a display-only value; do not use it as a verification secret. The same secret is available on the [webhooks settings page](https://sync.so/settings/webhooks).
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
client.organizations.get_webhook_secret()

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

**masked:** `typing.Optional[bool]` — When true, returns a display-only masked version of the secret that must not be used as a verification secret. Omit or set false when configuring a webhook verifier so you get the usable value.
    
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

## Projects
<details><summary><code>client.projects.<a href="src/sync/projects/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a project to group related generations and assets. Pass the returned id as projectId on POST /v2/generate or POST /v2/assets to file them under this project so they show up together in Studio. Only name is required — visibility defaults to USER and mode to CREATOR. Supply a client-generated UUID as id for idempotent creation. A retry with the same id returns the existing project and ignores other request fields; an id owned by another user/organization or a deleted project returns 409.
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
client.projects.create(
    id="612bb64a-e7f4-40c1-977b-3e9797845637",
    name="My API Project",
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

**name:** `str` — A name for the project.
    
</dd>
</dl>

<dl>
<dd>

**id:** `typing.Optional[str]` — Optional client-supplied project id (UUID) for idempotent creation. Re-sending the same id returns the existing project instead of creating a duplicate; the other request fields are ignored on such a replay. Fails with 409 if the id already belongs to a different user or organization, or to a deleted project.
    
</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — An optional description for the project.
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `typing.Optional[ProjectVisibility]` — Who can see the project. Defaults to USER (visible only to the owner).
    
</dd>
</dl>

<dl>
<dd>

**mode:** `typing.Optional[ProjectMode]` — The project mode. Defaults to CREATOR.
    
</dd>
</dl>

<dl>
<dd>

**default_workflow:** `typing.Optional[CreatorWorkflow]` — The default top-level creator workflow for this project.
    
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

<details><summary><code>client.projects.<a href="src/sync/projects/client.py">list</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the projects in your organization, most recently updated first.
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
client.projects.list(
    limit=10,
    sort_by="updatedAt",
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

**limit:** `typing.Optional[int]` — Maximum number of projects to return (1-100). Defaults to 10.
    
</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Cursor for pagination.
    
</dd>
</dl>

<dl>
<dd>

**search_query:** `typing.Optional[str]` — Search projects by name.
    
</dd>
</dl>

<dl>
<dd>

**sort_by:** `typing.Optional[ProjectSort]` — Sort order for the results. Defaults to updatedAt.
    
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

<details><summary><code>client.projects.<a href="src/sync/projects/client.py">get</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a project by id.
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
client.projects.get(
    id="612bb64a-e7f4-40c1-977b-3e9797845637",
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

**id:** `ProjectId` 
    
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

<details><summary><code>client.projects.<a href="src/sync/projects/client.py">attach_asset</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Attach an existing asset to a project so it is grouped under the project alongside its generations. The asset must belong to your organization and not be deleted. This is idempotent — re-attaching an asset that is already linked succeeds without creating a duplicate. Returns 204 No Content on success.
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
client.projects.attach_asset(
    id="612bb64a-e7f4-40c1-977b-3e9797845637",
    asset_id="8f14e45f-ceea-467d-9a1b-3e4d5c6f7a8b",
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

**id:** `ProjectId` 
    
</dd>
</dl>

<dl>
<dd>

**asset_id:** `AssetId` — The id of the asset to attach. The asset must belong to your organization and not be deleted.
    
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

<details><summary><code>client.projects.<a href="src/sync/projects/client.py">detach_asset</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Detach an asset from the project's draft content, such as its thumbnail. The asset remains in the project's asset library and keeps its access grants. Attaching it again restores the link. This operation is idempotent, including when the link is already detached or absent. Returns 204 No Content. An inaccessible project returns 404. An API key without an owner returns 422.
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
client.projects.detach_asset(
    id="id",
    asset_id="assetId",
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

**id:** `ProjectId` 
    
</dd>
</dl>

<dl>
<dd>

**asset_id:** `AssetId` 
    
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

<details><summary><code>client.projects.<a href="src/sync/projects/client.py">update</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update a project's name, description, visibility, or mode. Only the fields you provide are changed.
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
client.projects.update(
    id="612bb64a-e7f4-40c1-977b-3e9797845637",
    name="Renamed Project",
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

**id:** `ProjectId` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — A new name for the project.
    
</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — A new description for the project.
    
</dd>
</dl>

<dl>
<dd>

**visibility:** `typing.Optional[ProjectVisibility]` — Update who can see the project.
    
</dd>
</dl>

<dl>
<dd>

**mode:** `typing.Optional[ProjectMode]` — Update the project mode.
    
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

<details><summary><code>client.projects.<a href="src/sync/projects/client.py">delete</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a project. A project can't be deleted while any of its generations are queued or processing — wait for those to finish, then retry. Deletion soft-deletes the project and its generations, removes its asset links, and soft-deletes assets with no other active project. Assets linked to another active project are retained.
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
client.projects.delete(
    id="612bb64a-e7f4-40c1-977b-3e9797845637",
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

**id:** `ProjectId` 
    
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

## Transcriptions
<details><summary><code>client.transcriptions.<a href="src/sync/transcriptions/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Starts a word-level transcription of a window of a video, the first step of a dialogue edit. Provide exactly one of `sourceVideoUrl` or `sourceAudioUrl`, both hosted in sync. storage (upload via `POST /v2/assets/upload`). Passing pre-extracted audio skips the server-side download and transcode. Poll `GET /v2/transcriptions/{id}` until `status` is `COMPLETED`, then pass the `transcript` and your edits to `POST /v2/dialogue-edits`. An identical source and window returns the existing job instead of starting a new one. Transcription is not billed.
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
client.transcriptions.create(
    source_video_url="https://assets.sync.so/docs/example-video.mp4",
    end_ms=30000,
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

**source_video_url:** `typing.Optional[str]` — URL of the source video, hosted in sync. storage (upload it via POST /v2/assets/upload first). Provide exactly one of sourceVideoUrl or sourceAudioUrl.
    
</dd>
</dl>

<dl>
<dd>

**source_audio_url:** `typing.Optional[str]` — URL of audio already extracted from the source, hosted in sync. storage. Skips the server-side audio extraction. Provide exactly one of sourceVideoUrl or sourceAudioUrl.
    
</dd>
</dl>

<dl>
<dd>

**start_ms:** `typing.Optional[int]` — Start of the window to transcribe, in milliseconds from the start of the source. Defaults to 0.
    
</dd>
</dl>

<dl>
<dd>

**end_ms:** `typing.Optional[int]` — End of the window to transcribe, in milliseconds from the start of the source. Omit to transcribe to the end. The window cannot exceed 60 minutes.
    
</dd>
</dl>

<dl>
<dd>

**max_source_seconds:** `typing.Optional[int]` — Refuse the source if it is longer than this many seconds. Useful when a later step, such as a dialogue edit (10 minute window), cannot consume a longer transcript. Cannot exceed the endpoint ceiling of 3600 seconds.
    
</dd>
</dl>

<dl>
<dd>

**project_id:** `typing.Optional[ProjectId]` — Optional id of a project in your organization to file the job under.
    
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

<details><summary><code>client.transcriptions.<a href="src/sync/transcriptions/client.py">get</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the job status and, once `status` is `COMPLETED`, the word-level transcript. `COMPLETED` and `FAILED` are terminal; `error.code` says why a job failed.
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
client.transcriptions.get(
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

**id:** `TranscriptionJobId` — Transcription job id.
    
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

## Tts
<details><summary><code>client.tts.<a href="src/sync/tts/client.py">create</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Synthesize speech from a script and get back a hosted audio URL. The returned url can be reused as an audio input in POST /v2/generate to lip sync the synthesized take. voiceId accepts an ElevenLabs voice id (discover via GET /v2/voices) or the id of a voice cloned via POST /v2/voices. Free-tier keys share the monthly ElevenLabs allowance; paid plans are billed per use.

A voiceId that does not resolve returns a 422 with errorCode voice_not_found. If a voice from your own ElevenLabs account stops resolving, the connected API key may be invalid — provider failures surface errorCode elevenlabs_api_key_invalid (reconnect it in Settings > Integrations) or elevenlabs_quota_exceeded (402) when your own ElevenLabs quota is exhausted. Temporary ElevenLabs provider failures return errorCode elevenlabs_service_unavailable: 504 for provider timeouts and 503 for other provider outages. Retry those requests with backoff and include the requestId if you contact support. A voice with an unresolved ElevenLabs restriction returns errorCode voice_verification_required or voice_blocked (both normally 422, or 400 when the pre-synthesis check was unavailable), or voice_access_denied (400). The required action depends on the code and on whether the voice is from your own connected ElevenLabs account — see the Error Handling guide.
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
client.tts.create(
    script="Hey — thanks for trying sync. labs.",
    voice_id="EXAVITQu4vr4xnSDxMaL",
    provider="elevenlabs",
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

**script:** `str` — The text to synthesize into speech (1–5,000 characters).
    
</dd>
</dl>

<dl>
<dd>

**voice_id:** `str` — A voice id to synthesize with — either an ElevenLabs voice id (discover via GET /v2/voices) or the id of a voice cloned via POST /v2/voices.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `VoiceProvider` — The voice provider to synthesize with. Currently `elevenlabs`.
    
</dd>
</dl>

<dl>
<dd>

**stability:** `typing.Optional[float]` — Voice stability (0-1). Higher is more consistent, lower is more expressive.
    
</dd>
</dl>

<dl>
<dd>

**similarity_boost:** `typing.Optional[float]` — How closely the synthesized audio matches the original voice (0-1).
    
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

<details><summary><code>client.tts.<a href="src/sync/tts/client.py">create_job</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit a job for asynchronous speech synthesis. Returns 202 with the accepted job and a `Location` header pointing at GET /v2/tts/jobs/{id}; poll that endpoint for the result. Accepts the same body as POST /v2/tts. API-key requests require your organization to be enabled for the asynchronous TTS rollout; otherwise the request returns 503.
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
client.tts.create_job(
    script="Hey — thanks for trying sync. labs.",
    voice_id="EXAVITQu4vr4xnSDxMaL",
    provider="elevenlabs",
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

**script:** `str` — The text to synthesize into speech (1–5,000 characters).
    
</dd>
</dl>

<dl>
<dd>

**voice_id:** `str` — A voice id to synthesize with — either an ElevenLabs voice id (discover via GET /v2/voices) or the id of a voice cloned via POST /v2/voices.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `VoiceProvider` — The voice provider to synthesize with. Currently `elevenlabs`.
    
</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `typing.Optional[str]` — Optional idempotency key, 1–128 characters after trimming. Reusing the same key within your organization returns the original job; reusing it with a different request body returns 409.
    
</dd>
</dl>

<dl>
<dd>

**stability:** `typing.Optional[float]` — Voice stability (0-1). Higher is more consistent, lower is more expressive.
    
</dd>
</dl>

<dl>
<dd>

**similarity_boost:** `typing.Optional[float]` — How closely the synthesized audio matches the original voice (0-1).
    
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

<details><summary><code>client.tts.<a href="src/sync/tts/client.py">get_job</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a text-to-speech job by id. While the job is PENDING or PROCESSING, the response carries a `Retry-After: 3` header. The header is absent once the job reaches a terminal state (SUCCESS or FAILED).
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
client.tts.get_job(
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

**id:** `str` — The job id returned when the job was submitted.
    
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

## Voices
<details><summary><code>client.voices.<a href="src/sync/voices/client.py">list</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the voices available to your organization — built-in ElevenLabs voices plus any you have cloned. Use a voice's id as voiceId in POST /v2/tts and in generation text inputs. A voice that carries a `restriction` cannot currently synthesize speech — check `restriction` and choose another voice. Voice availability can change over time, so re-check it rather than assuming a voice stays usable.
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
client.voices.list()

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

**provider:** `typing.Optional[VoiceProvider]` — Filter voices by provider. Currently `elevenlabs`.
    
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

<details><summary><code>client.voices.<a href="src/sync/voices/client.py">get</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a single voice by the same id values GET /v2/voices exposes — a built-in ElevenLabs voice id or the UUID of a voice cloned by your organization. A missing or foreign-organization id returns a 404 with errorCode voice_not_found.
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
client.voices.get(
    id="EXAVITQu4vr4xnSDxMaL",
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

**id:** `str` — The voice id — a built-in provider voice id or a cloned voice UUID.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `typing.Optional[VoiceProvider]` — Provider to resolve the voice against. Currently `elevenlabs`.
    
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

<details><summary><code>client.voices.<a href="src/sync/voices/client.py">clone</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Clone a custom voice from an audio or video sample and get back its id for use in POST /v2/tts and generation text inputs.

The exact sequence for a local file: (1) request a presigned URL via POST /v2/assets/upload, (2) PUT the file bytes to the returned uploadUrl, (3) clone from the returned url (or register it via POST /v2/assets and clone from the assetId). Samples must be hosted in sync. labs storage — external URLs are rejected with errorCode voice_sample_upload_required. Video sources have their audio track extracted automatically (first 2 minutes). Video sources staged for extraction are limited to 1 GiB (1,073,741,824 bytes); larger sources return 413 voice_sample_source_too_large. This endpoint allows 10 requests per hour per API key (or per signed-in user).

For best results use 30 seconds to 2 minutes of clear, single-speaker speech without background music or noise. Samples that are too short are rejected with errorCode voice_sample_too_short. Clone slots are limited per plan (403 voice_clone_limit_reached) and voice names must be unique within your organization (409 voice_name_conflict). Sample source problems return 422 (voice_sample_not_accessible, voice_sample_type_unsupported, voice_sample_upload_required, voice_sample_extraction_failed); invalid or too-short samples return 400 (voice_sample_invalid, voice_sample_too_short). A 429 may mean the request-rate limit was exceeded or shared provider capacity is busy (voice_clone_busy); follow the response retry guidance. Provider outages return 503 (elevenlabs_service_unavailable).
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
client.voices.clone(
    name="My Narrator",
    provider="elevenlabs",
    asset_id="550e8400-e29b-41d4-a716-446655440000",
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

**name:** `str` — A name for the cloned voice, 1–100 characters. Names starting with edit-dialogue- after trimming whitespace and ignoring case are reserved.
    
</dd>
</dl>

<dl>
<dd>

**provider:** `VoiceProvider` — The provider to clone the voice with. Currently `elevenlabs`.
    
</dd>
</dl>

<dl>
<dd>

**url:** `typing.Optional[str]` — A sync. labs-hosted url of the audio or video sample to clone from. Provide exactly one of `url`, `assetId` or `sampleUrls`.
    
</dd>
</dl>

<dl>
<dd>

**asset_id:** `typing.Optional[str]` — The id of a previously uploaded audio or video asset to clone from. Provide exactly one of `url`, `assetId` or `sampleUrls`.
    
</dd>
</dl>

<dl>
<dd>

**sample_urls:** `typing.Optional[typing.Sequence[str]]` — 1 to 10 sync. labs-hosted urls of audio or video samples of the same voice, cloned together. Provide exactly one of `url`, `assetId` or `sampleUrls`.
    
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

<details><summary><code>client.voices.<a href="src/sync/voices/client.py">delete</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a cloned voice, freeing a clone slot. Unknown ids return 404 with errorCode `voice_not_found`.
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
client.voices.delete(
    id="7f9c2b3a-1d4e-4a8b-9c0d-2e3f4a5b6c7d",
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

**id:** `str` — The Sync UUID returned as id when the voice was cloned.
    
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

