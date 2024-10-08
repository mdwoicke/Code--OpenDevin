# Azure OpenAI LLM

## Completion

OpenHands uses LiteLLM for completion calls. You can find their documentation on Azure [here](https://docs.litellm.ai/docs/providers/azure)

### Azure openai configs

When running the OpenHands Docker image, you'll need to set the following environment variables using `-e`:

```
LLM_BASE_URL="<azure-api-base-url>"          # e.g. "https://openai-gpt-4-test-v-1.openai.azure.com/"
LLM_API_KEY="<azure-api-key>"
LLM_MODEL="azure/<your-gpt-deployment-name>"
LLM_API_VERSION="<api-version>"          # e.g. "2024-02-15-preview"
```

Example:
```bash
docker run -it \
--pull=always \
-e SANDBOX_USER_ID=$(id -u) \
-e WORKSPACE_MOUNT_PATH=$WORKSPACE_BASE \
-e LLM_BASE_URL="x.openai.azure.com" \
-e LLM_API_VERSION="2024-02-15-preview" \
-v $WORKSPACE_BASE:/opt/workspace_base \
-v /var/run/docker.sock:/var/run/docker.sock \
-p 3000:3000 \
--add-host host.docker.internal:host-gateway \
--name openhands-app-$(date +%Y%m%d%H%M%S) \
ghcr.io/all-hands-ai/openhands:main
```

You can set the LLM_MODEL and LLM_API_KEY in the OpenHands UI itself.

:::note
You can find your ChatGPT deployment name on the deployments page in Azure. It could be the same with the chat model name (e.g. 'GPT4-1106-preview'), by default or initially set, but it doesn't have to be the same. Run openhands, and when you load it in the browser, go to Settings and set model as above: "azure/&lt;your-actual-gpt-deployment-name&gt;". If it's not in the list, enter your own text and save it.
:::

## Embeddings

OpenHands uses llama-index for embeddings. You can find their documentation on Azure [here](https://docs.llamaindex.ai/en/stable/api_reference/embeddings/azure_openai/)

### Azure openai configs

The model used for Azure OpenAI embeddings is "text-embedding-ada-002".
You need the correct deployment name for this model in your Azure account.

When running OpenHands in Docker, set the following environment variables using `-e`:

```
LLM_EMBEDDING_MODEL="azureopenai"
LLM_EMBEDDING_DEPLOYMENT_NAME="<your-embedding-deployment-name>"        # e.g. "TextEmbedding...<etc>"
LLM_API_VERSION="<api-version>"         # e.g. "2024-02-15-preview"
```
