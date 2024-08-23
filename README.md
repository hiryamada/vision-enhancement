# GPT-4 "Vision enhancement" with images

As of August 2024, the vision enhancement doesn't work in the old Azure OpenAI Studio experience, and the new experience doesn't seem to provide a switch to use the vision enhancement.

So I developed this sample that uses a Visual Studio Code extension to send an HTTP request.

reference: https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/gpt-with-vision?tabs=rest%2Csystem-assigned%2Cresource#use-vision-enhancement-with-images


## API versions difference

Please note that some paths and property names may differ depending on the API version used.

|API version|path|data sources|
|-|-|-|
|`2023-12-01-preview`|`/extensions/chat/completions`|`dataSources`|
|`2024-02-25-preview`|`/chat/completions`|`data_sources`|

## Azure resources

Create 2 resources in the same region. For example:

Azure OpenAI Service
- region: westus

Azure AI Computer Vision
- region: westus
- level: paid (S1) tier

## Model deployment

Create a deployment using Azure OpenAI Studio.

- model name: gpt-4
- model version: vision-preview

## Visual Studio Code extension

Install the REST Client extension.

https://marketplace.visualstudio.com/items?itemName=humao.rest-client

## .env file

Copy `.env.sample` to `.env` and adjust it for your resource name/key/endpoint and image URL you want to analyze.

## Send HTTP request

Open `.http` file and click 'Send Request'.

## Sample response body

```json
{
  "choices": [
    {
      "content_filter_results": {
        "hate": {
          "filtered": false,
          "severity": "safe"
        },
        "self_harm": {
          "filtered": false,
          "severity": "safe"
        },
        "sexual": {
          "filtered": false,
          "severity": "safe"
        },
        "violence": {
          "filtered": false,
          "severity": "safe"
        }
      },
      "finish_reason": "length",
      "index": 0,
      "message": {
        "content": "You are looking at an image of a cat lying down on a wooden floor. The cat has a short fur coat with a distinctive pattern of white, grey, and brown patches. It has striking eyes and a calm demeanor, looking directly at the camera. Beside the cat, there appears to be a woven basket or container of some sort, partially visible in the background. The setting is indoors, with a warm tone to the ambient lighting, possibly from sunlight. The space under furniture can be seen",
        "role": "assistant"
      },
      "enhancements": {
        "grounding": {
          "lines": [
            {
              "text": "You are looking at an image of a cat lying down on a wooden floor. The cat has a short fur coat with a distinctive pattern of white, grey, and brown patches. It has striking eyes and a calm demeanor, looking directly at the camera. Beside the cat, there appears to be a woven basket or container of some sort, partially visible in the background. The setting is indoors, with a warm tone to the ambient lighting, possibly from sunlight. The space under furniture can be seen",
              "spans": [
                {
                  "text": "the cat",
                  "length": 7,
                  "offset": 67,
                  "polygon": [
                    {
                      "x": 0.16449999809265137,
                      "y": 0.23149999976158142
                    },
                    {
                      "x": 0.9975000023841858,
                      "y": 0.23149999976158142
                    },
                    {
                      "x": 0.9975000023841858,
                      "y": 0.8005000352859497
                    },
                    {
                      "x": 0.16449999809265137,
                      "y": 0.8005000352859497
                    }
                  ]
                },
                {
                  "text": "eyes",
                  "length": 4,
                  "offset": 174,
                  "polygon": [
                    {
                      "x": 0.22550000250339508,
                      "y": 0.3855000138282776
                    },
                    {
                      "x": 0.37950000166893005,
                      "y": 0.3855000138282776
                    },
                    {
                      "x": 0.37950000166893005,
                      "y": 0.4505000412464142
                    },
                    {
                      "x": 0.22550000250339508,
                      "y": 0.4505000412464142
                    }
                  ]
                },
                {
                  "text": "the cat",
                  "length": 7,
                  "offset": 239,
                  "polygon": [
                    {
                      "x": 0.16449999809265137,
                      "y": 0.23149999976158142
                    },
                    {
                      "x": 0.9975000023841858,
                      "y": 0.23149999976158142
                    },
                    {
                      "x": 0.9975000023841858,
                      "y": 0.8005000352859497
                    },
                    {
                      "x": 0.16449999809265137,
                      "y": 0.8005000352859497
                    }
                  ]
                }
              ]
            }
          ],
          "status": "Success"
        }
      }
    }
  ],
  "created": 1724379197,
  "id": "chatcmpl-9zE5dtLJp5ifFFOm5DGXGnI0m8xBk",
  "model": "gpt-4",
  "object": "chat.completion",
  "prompt_filter_results": [
    {
      "prompt_index": 0,
      "content_filter_results": {
        "hate": {
          "filtered": false,
          "severity": "safe"
        },
        "self_harm": {
          "filtered": false,
          "severity": "safe"
        },
        "sexual": {
          "filtered": false,
          "severity": "safe"
        },
        "violence": {
          "filtered": false,
          "severity": "safe"
        }
      }
    }
  ],
  "usage": {
    "completion_tokens": 100,
    "prompt_tokens": 786,
    "total_tokens": 886
  }
}
```
