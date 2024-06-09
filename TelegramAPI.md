### sendMessage

Use this method to send text messages. On success, the sent Message is returned.

  

|Parameter|Type|Required|Description|
|--|--|--|--|
|business_connection_id|String|Optional Unique identifier of the business connection on behalf of which the message will be sent|
|chat_id|Integer or String|YesUnique identifier for the target chat or username of the target channel (in the format @channelusername)
|message_thread_id  Integer Optional    Unique identifier for the target message thread (topic) of the forum; for forum supergroups only

|text   String  Yes Text of the message to be sent, 1-4096 characters after entities parsing

|parse_mode String  Optional    Mode for parsing entities in the message text. See formatting options for more details.

|entities   Array of MessageEntity  Optional    A JSON-serialized list of special entities that appear in message text, which can be specified instead of parse_mode

|link_preview_options   LinkPreviewOptions  Optional    Link preview generation options for the message

|disable_notification   Boolean Optional    Sends the message silently. Users will receive a notification with no sound.

|protect_content    Boolean Optional    Protects the contents of the sent message from forwarding and saving

|message_effect_id  String  Optional    Unique identifier of the message effect to be added to the message; for private chats only

|reply_parameters   ReplyParameters Optional    Description of the message to reply to

|reply_markup   InlineKeyboardMarkup or ReplyKeyboardMarkup or ReplyKeyboardRemove or ForceReply    Optional    Additional interface options. A JSON-serialized object for an inline keyboard, custom reply keyboard, instructions to remove a reply keyboard or to force a reply from the user