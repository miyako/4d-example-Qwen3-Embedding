## [Qwen/Qwen3-Embedding-0.6B](https://huggingface.co/Qwen/Qwen3-Embedding-0.6B)

**Qwen3 Embedding** is a decoder-only text embedding model released by **Alibaba** in 2025.

|`max_position_embeddings`|`hidden_size`|`num_hidden_layers`|`pooling`
|-:|-:|-:|-:|
|`32768`|`1024`|`28`|`last`

```4d
var $AIClient : cs.AIKit.OpenAI
$AIClient:=cs.AIKit.OpenAI.new()

$AIClient.baseURL:="http://127.0.0.1:8080/v1"  // llama-server

$query:="Instruct: Retrieve text that answers the question\nQuery: "+"What is the TCP port number used by 4D Server?"

var $batch : cs.AIKit.OpenAIEmbeddingsResult
$batch:=$AIClient.embeddings.create($query)

If ($batch.success)
	$vector:=$batch.embedding.embedding
	var $comparison:={vector: $vector; metric: mk cosine; threshold: 0.6}
	var $results:=ds.Documents.query("Embeddings > :1"; $comparison)
	If ($results.length#0)
		ALERT($results.first().Text)
	End if 
End if
```

<img width="480" height="542" alt="" src="https://github.com/user-attachments/assets/442fe6c5-e720-4ea6-9909-a23b747d3380" />
