### Dialogue

A dialogue system in Lua / LÖVE (Love2D) typically involves:

- Storing dialogue

- Use JSON (.json), Lua tables (.lua), or plain text (.txt or .csv).
  JSON is widely used for structured data and is easy to parse.
  Lua tables can be directly loaded as a script.
  Plain text or CSV files work for simple structures but require custom parsing.
  Loading dialogue

- Read the file and parse its contents (using `json.lua` for JSON or `love.filesystem.read` for text).
  Convert data into a usable format (e.g., a table with character names, text, choices).
  Displaying dialogue

- Render text on the screen using `love.graphics.print()`.
  Implement a system for advancing dialogue (e.g., pressing a key to go to the next line).
  Handle branching choices if needed.

---

1. Create a `dialogue.json` file.

```json
{
  "1": {
    "speaker": "NPC",
    "text": "Hello, traveler! What brings you here?",
    "choices": {
      "A": { "text": "I'm just looking around.", "next": "2" },
      "B": { "text": "None of your business.", "next": "3" }
    }
  },
  "2": {
    "speaker": "NPC",
    "text": "Well, enjoy your stay!",
    "choices": {}
  },
  "3": {
    "speaker": "NPC",
    "text": "Alright, no need to be rude.",
    "choices": {}
  }
}
```

2. Use a JSON library like [json.lua](https://github.com/rxi/json.lua). Place it in your project folder.

```lua
-- main.lua
local json = require "json"

function love.load()
    local file = love.filesystem.read("dialogue.json")
    dialogueData = json.decode(file)
    currentDialogueId = "1" -- Start from the first dialogue
end
```

3. In `love.draw`:

```lua
function love.draw()
    local dialogue = dialogueData[currentDialogueId]

    if dialogue then
        love.graphics.print(dialogue.speaker .. ": " .. dialogue.text, 50, 50)

        -- Display choices
        local yOffset = 100
        for key, choice in pairs(dialogue.choices) do
            love.graphics.print(key .. ": " .. choice.text, 50, yOffset)
            yOffset = yOffset + 20
        end
    end
end
```

4.In `love.keypressed()`:

```lua
function love.keypressed(key)
    local dialogue = dialogueData[currentDialogueId]

    if dialogue and dialogue.choices[key] then
        currentDialogueId = dialogue.choices[key].next
    end
end
```
