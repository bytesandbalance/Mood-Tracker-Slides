---
layout: section
background: black
theme: dracula
---

# Final Project - Adding a Chat Interface for Mood Support

---
layout: default
---

Alright, it's time to wrap things up with a cool project! You’re going to create a chat interface for mood support in your mobile app. Here's what you need to do:

1. **Sign up for ChatGPT**
2. **Use ChatGPT for help on creating a chat interface**
3. **Use ChatGPT for help on integrating the chat interface into the app**
4. **Get and use your ChatGPT API key**

---
layout: default
---

# 1. Signing Up for ChatGPT

First things first, you need to sign up for ChatGPT. Just follow these steps:

- Head over to [ChatGPT's website](https://www.openai.com/chatgpt) and sign up.
- Follow the instructions to complete the registration.
- Once you’re in, you can start asking ChatGPT for help.


---
layout: default
---

# 2. Using ChatGPT for Help on Creating a Chat Interface

You can ask ChatGPT to guide you through creating a chat interface. Here's an example of how to ask for help:

**Example Conversation:**

```plaintext
Student: I need help creating a chat interface for my mobile app. Can you guide me through the process?

ChatGPT: Of course! Here’s a basic outline to create a chat interface:
1. Choose a framework or library for the chat interface (e.g., React Native for mobile apps).
2. Set up the initial project structure.
3. Create the chat UI components, like chat bubbles, input fields, and send buttons.
4. Implement state management to handle user input and chat history.
5. Integrate a backend service to store and retrieve chat messages.
Would you like more detailed steps on any of these points?
```

---
layout: default
---


**Prompt Engineering Tips:**

- Be specific. Instead of asking "How do I create a chat interface?", ask "Can you give me step-by-step instructions for creating a chat interface using React Native?"
- If you need more details, ask follow-up questions.
- Test as you go: build a small part, test it, then ask ChatGPT for the next steps.

---
layout: default
---

**Example Code Snippet:**

````md magic-move
```js
import React, { useState } from 'react';
import { View, TextInput, Button, FlatList, Text } from 'react-native';
```
```js
const ChatInterface = () => {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState('');

  const sendMessage = () => {
    setMessages([...messages, { key: messages.length.toString(), text: input }]);
    setInput('');
  };

  return (
    <View style={{ flex: 1, padding: 20 }}>
      <FlatList
        data={messages}
        renderItem={({ item }) => <Text>{item.text}</Text>}
      />
      <TextInput
        value={input}
        onChangeText={setInput}
        style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
      />
      <Button title="Send" onPress={sendMessage} />
    </View>
  );
};
```
```js
export default ChatInterface;
```
````

---
layout: default
---


# 3. Using ChatGPT for Help on Integrating the Chat Interface into The App

Now that you have the chat interface, let’s integrate it into the app. ChatGPT can help with this too. Here's another example conversation:

# Example Conversation

```plaintext
Student: I have created a chat interface for mood support. How do I integrate this into my existing mobile app?

ChatGPT: Great to hear you’ve created the chat interface! Here’s how you can integrate it:
1. Import the chat interface components into your main app component.
2. Add navigation to the app so users can access the chat feature.
3. Ensure that your app’s state management can handle chat data.
4. Test the integration thoroughly to make sure the chat feature works seamlessly with the rest of the app.
Do you need help with any specific part of the integration process?
```

---
layout: default
---

# Example Code Snippet for Integration

```js
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen';
import ChatInterface from './ChatInterface';

const Stack = createStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Chat" component={ChatInterface} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
```

---
layout: default
---

# 4. Getting and Using Your ChatGPT API Key

To use ChatGPT's NLP powers in the app, you’ll need an API key. Here’s how to get and use it:

- Log in to your OpenAI account.
- Go to [the API section](https://platform.openai.com/api-keys) and generate a new API key.
- Copy the API key and keep it safe.


---
layout: default
---

# Example Conversation for Using the API

```plaintext
Student: I have my API key. How do I use it to integrate ChatGPT's NLP capabilities into my app?

ChatGPT: Great! Here’s a simple example of how to use the ChatGPT API in a JavaScript environment:
1. Install Axios for making HTTP requests: `npm install axios`
2. Use the following code snippet to make a request to the ChatGPT API:
```

---
layout: default
---

# Example Code Snippet for Using ChatGPT API

````md magic-move
```js
import axios from 'axios';

const API_KEY = 'your-api-key-here';
const API_URL = 'https://api.openai.com/v1/engines/davinci-codex/completions';
```
```js
const getChatGPTResponse = async (prompt) => {
  try {
    const response = await axios.post(
      API_URL,
      {
        prompt: prompt,
        max_tokens: 150,
      },
      {
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${API_KEY}`,
        },
      }
    );
    return response.data.choices[0].text.trim();
  } catch (error) {
    console.error('Error getting response from ChatGPT:', error);
    return 'Error getting response from ChatGPT';
  }
};
```
```js
// Example usage
const userPrompt = 'What is the capital of France?';
getChatGPTResponse(userPrompt).then(response => {
  console.log('ChatGPT response:', response);
});
```
````
---
layout: default
---

# Testing Your Integration

- Test the chat feature separately first.
- Perform integration testing to ensure the chat feature works well with the rest of the app.
- Ask ChatGPT for help if you hit any issues.

---
layout: default
---

# Example Conversation for Testing

```plaintext
Student: My chat interface works, but after integrating it into my app, the navigation stops working.
Can you help me debug this issue?
ChatGPT: Let’s debug this step by step.
First, check if the navigation library is properly configured and imported in your main app component.
Ensure there are no conflicting routes or navigation states.
Here’s a checklist to help you diagnose the problem...
```

---
layout: default
---

# Summary

- Understand the framework you're using to help debug, as ChatGPT can get confused and make mistakes. Always test everything yourself and don't believe everything blindly.
- Learn how to do prompt engineering effectively to get accurate responses and ensure your project works smoothly.