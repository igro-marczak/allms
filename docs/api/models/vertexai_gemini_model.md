---
layout: default
title: VertexAIGeminiModel
parent: Models
grand_parent: API
nav_order: 4
---

## `class llm_wrapper.models.VertexAIGeminiModel` API
### Methods
```python
__init__(
    temperature: float = 0.0,
    top_k: int = 40,
    top_p: float = 0.95,
    max_output_tokens: int = 1024,
    model_total_max_tokens: int = 8192,
    max_concurrency: int = 1000,
    max_retries: int = 8,
    verbose: bool = True
)
```
#### Parameters
- `temperature` (`float`): The sampling temperature, between 0 and 1. Higher values like 0.8 will make the output more
   random, while lower values like 0.2 will make it more focused and deterministic. Default: `0.0`.
- `top_k` (`int`): Changes how the model selects tokens for output. A top-k of 3 means that the next token is selected
   from among the 3 most probable tokens. Default: `40`.
- `top_p` (`float`): Top-p changes how the model selects tokens for output. Tokens are selected from most probable to
   least until the sum of their probabilities equals the top_p value. Default: `0.95`.
- `max_output_tokens` (`int`): The maximum number of tokens to generate by the model. The total length of input tokens 
   and generated tokens is limited by the model's context length. Default: `1024`.
- `model_total_max_tokens` (`int`): Context length of the model - maximum number of input plus generated tokens. Default: `8192`.
- `max_concurrency` (`int`): Maximum number of concurrent requests. Default: `1000`.
- `max_retries` (`int`): Maximum number of retries if a request fails. Default: `8`.
- `verbose` (`bool`): Default: `True`.

---

```python
generate(
    prompt: str,
    input_data: typing.Optional[typing.List[InputData]] = None,
    output_data_model_class: typing.Optional[typing.Type[BaseModel]] = None
) -> typing.List[ResponseData]:
```
#### Parameters
- `prompt` (`str`): Prompt to use to query the model.
- `input_data` (`Optional[List[InputData]]`): If prompt contains symbolic variables you can use this parameter to
   generate model responses for batch of examples. Each symbolic variable from the prompt should have mapping provided
   in the `input_mappings` of `InputData`.
- `output_data_model_class` (`Optional[Type[BaseModel]]`): If provided forces the model to generate output in the
  format defined by the passed class. Generated response is automatically parsed to this class.

#### Returns
`List[ResponseData]`: Each `ResponseData` contains the response for a single example from `input_data`. If `input_data`
is not provided, the length of this list is equal 1, and the first element is the response for the raw prompt. 

---

```python
VertexAIGeminiModel.setup_environment(
    gcp_project_id: str,
    gcp_llm_region: str,
    gcp_model_name: str = "gemini-pro"
)
```
#### Parameters
- `gcp_project_id` (`str`): The GCP project to use when making Vertex API calls.
- `gcp_llm_region` (`str`): The region to use when making API calls.
- `gcp_model_name` (`str`): Default: `"gemini-pro"`.

---

### Example usage
```python
from llm_wrapper.models import VertexAIGeminiModel 
from llm_wrapper.domain.configuration import VertexAIConfiguration

configuration = VertexAIConfiguration(
    cloud_project="<GCP_PROJECT_ID>",
    cloud_location="<MODEL_REGION>"
)

vertex_model = VertexAIGeminiModel(config=configuration)
vertex_response = vertex_model.generate("2+2 is?")
```