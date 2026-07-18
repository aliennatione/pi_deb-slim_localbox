# Pi4PocketLLM

## Build debian container
You can build the image with ´docker build -t pi_local-sandbox_debian -f Dockerfile-debian_pi .´

## Download a model
For example:

```sh
mkdir models/gemma-4-E2B_q4_0-it
curl -LsSf https://huggingface.co/google/gemma-4-E2B-it-qat-q4_0-gguf/resolve/main/gemma-4-E2B_q4_0-it.gguf -o models/gemma-4-E2B_q4_0-it.gguf
curl -LsSf https://huggingface.co/google/gemma-4-E2B-it-qat-q4_0-gguf/resolve/main/gemma-4-E2B-it-mmproj.gguf -o gemma-4-E2B-it-mmproj.gguf
```

## Run container and enter in it
```sh
docker run --rm -it \
  -e ENDPOINT_API_URL=192.168.1.84 \
  -v "./llama-b10066:/root/llama" \
  -v "./workspace:/workspace" \
  -v "./models:/root/models" \
  -v "./pi-agent-home:/root/.pi/agent" \
  pi_local-sandbox_debian
```

## Serve llama without --model or -m or passing a model starts single-model mode instead of router mode
In the container:
```sh
llama serve \
  --models-dir ~/models \
  --no-models-autoload \
  --jinja \
  --host 127.0.0.1 \
  --port 8080 \
  -c 32768 \
  -m gemma-4-E2B_q4_0-it &
```

## Install pi-llama plugin
`pi install /root/pi-llama`

# 3. Run Pi
Everything is set, simply run:

`pi`
