This is example how to send a message with a premium emoji using Telethon in Python.


## Usage
```python
from telethon import TelegramClient
from xtelethon import CustomParseMode  # TODO: Call the custom class

# TODO: Change with your own values
API_ID = 12345678
API_HASH = 'x393637bjp62c7b.........'
SESSION = 'my_session.session'

client = TelegramClient(SESSION, API_ID, API_HASH).start()
client.parse_mode = CustomParseMode('markdown')  # TODO: Choose parsemode


async def main():
    # TODO: Change the emoji id as well as its corespoding emoji
    msg = 'hello this is a [Text](spoiler), with custom emoji [❤️](emoji/10002345) !'
    await client.send_message('me', msg)  # Send message to your own account/Saved Messages
    await client.disconnect()


with client:
    client.loop.run_until_complete(main())
```



## Example - How to get emoji ID
```python
from telethon import TelegramClient, events
from telethon.tl.types import MessageEntityCustomEmoji

# TODO: Replace the placeholders with your own values
API_ID = 98765432
API_HASH = 'x17f7ce903s17bxf3......'
SESSION = 'my_telethon_session.session'

client = TelegramClient(SESSION, API_ID, API_HASH).start()


@client.on(events.NewMessage(from_users='me'))
async def handler(event):
    message_text = event.message.message
    custom_emojis = []

    if event.entities:
        for entity in event.entities:
            if isinstance(entity, MessageEntityCustomEmoji):
                emoji = message_text[entity.offset:entity.offset + entity.length]
                custom_emojis.append((emoji, entity.document_id))

    for emoji, emoji_id in custom_emojis:
        # Print the emoji's ID and the corresponding emoji character
        print(f"Custom Emoji ID: {emoji_id} | {emoji}")

print("\n― Please send Premium Emoji to your 'Saved Messages'\n― Listening for messages...\n")
client.run_until_disconnected()
```
