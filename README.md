# Discollama

`discollama` is a Discord bot powered by a local large language model backed by [Ollama](https://github.com/ollama/ollama).

## Dependencies

- Docker, Docker Compose, Portainer

## Installation

On host machine create a file directly where you want to clone the directory to that is easy to located, I use a folder called portainer to hold all my containers so it would look like
```ruby
EXAMPLE
/home/USER/portainer/discollama
```
Clone the repository into your desired folder (note that clone will create a folder)
```ruby
git clone https://github.com/BadgerSnacks/discollama-portainer.git
```
Copy the contents of the compose.ymal into your portainer web editor, You will need to edit your compose.ymal file to match the file structure 
```ruby
EXAMPLE
volumes:
      - YOUR FILE DIRECTORY

dockerfile: FILE DIRECTORY THAT DOCKERFILE IS LOCATED

change to

volumes:
      - /home/USER/portainer/discollama:/discollama

dockerfile: /home/USER/portainer/discollama/Dockerfile
```
Make sure you update all 3 areas for file locations in the compose.ymal file.

> [!NOTE]
> You must setup a [Discord Bot](https://discord.com/developers/applications) and set environment variable `DISCORD_TOKEN` before `discollama.py` can access Discord.

In poratiner you will need to add your discord token into an environment variable. While under the editor tab of your stack scroll down and find Environment Variables dropdown menu, click Advanced mode and enter your discord token.
```
EXAMPLE
DISCORD_TOKEN=################
```

After you succsessfully deply the stack you will need intall your models as they are not pulled yet, defualt is set to llama3.2. there are two ways to do this.

From the container terminal
```ruby
ollama pull llama3.2
```
From bash(terminal) outside of the container
```ruby
docker exec -it ollama ollama pull llama3.2
```

## Customize `discollama.py`

A custom personality can be added by changing the `SYSTEM` instruction in the Modelfile and running `ollama create`:

```
ollama create mymodel -f Modelfile
```

This can be changed in `compose.yaml`:

```
environment:
  - OLLAMA_MODEL=mymodel
```
You should be able to update this environment to change any to any other ollama models you have pulled. I have only tested with 1 model as of now.

See [ollama/ollama](https://github.com/ollama/ollama/blob/main/docs/modelfile.md) for more details.

## Activating the Bot

Discord users can interact with the bot by mentioning it in a message to start a new conversation or in a reply to a previous response to continue an ongoing conversation.
