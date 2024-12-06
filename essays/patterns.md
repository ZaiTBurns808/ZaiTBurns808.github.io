---
layout: essay
type: essay
title: "Patterns Do More For Engineers Than You'd Think"
date: 2024-12-05
published: true
labels:
  - Software Engineering
  - Design Patterns
---

<img width="500px" class="rounded float-start pe-4" src="../img/Eng.png">

*Design patterns: reusable solutions to common problems in software development.*

## Introduction

Engineering, in all its forms, is often a discipline defined by its practitioners’ ability to tackle complex problems with innovative solutions. Software engineering is no different. At its core, the profession involves identifying requirements and crafting unique solutions to meet them. However, even in this innovative field, common and proven approaches exist, streamlining problem-solving and boosting efficiency. These approaches, known as **design patterns**, provide reusable, effective templates for solving recurring problems.

Before exploring the concept further, my understanding of design patterns was limited to their definition as templates for efficient and maintainable software development. However, I did not realize how these patterns are categorized or how they already appear in my own code. Through further exploration and assistance from my favorite AI (ChatGPT), I identified two design patterns I inadvertently applied in a recent project—building an RSA encryption system for a hypothetical messaging application.

## The Factory Method Pattern

The **factory method pattern** provides an interface for creating objects but delegates the instantiation decision to subclasses or methods. This design ensures that the object creation logic is encapsulated and abstracted away, making the system more modular and maintainable.

### Example from My Code: `addNode` Method

In my project, the `CommunicationGraph` class employs the factory method pattern. The `addNode` method encapsulates the creation logic for `Node` objects, ensuring other parts of the code remain agnostic to the specifics of node creation.

```java
class CommunicationGraph {
    private final Map<String, Node> nodes;

    public CommunicationGraph() {
        this.nodes = new HashMap<>();
    }

    // Factory method for creating and adding a Node
    public Node addNode(String id) throws NoSuchAlgorithmException {
        Node node = new Node(id); // Encapsulated creation logic
        nodes.put(id, node);      // Adds the node to the graph
        return node;
    }
}

// Usage
CommunicationGraph graph = new CommunicationGraph();
Node alice = graph.addNode("Alice");
```
By encapsulating the creation logic, this method adheres to the factory method pattern, simplifying object instantiation and ensuring scalability in more complex systems.

## The Builder Pattern
The builder pattern constructs complex objects step by step, separating the construction process from the object representation. This allows for greater flexibility and clarity, particularly when dealing with optional parameters.
### Example from My Code: `Message` Class
Although my implementation does not currently leverage the full potential of the builder pattern, the Message class is structured to support this design, particularly for cases requiring optional parameters like metadata or ID.
```java
class Message {
    private final String sender;
    private final String receiver;
    private final String metadata;
    private final String body;

    private Message(String sender, String receiver, String metadata, String body) {
        this.sender = sender;
        this.receiver = receiver;
        this.metadata = metadata;
        this.body = body;
    }

    // Builder class for constructing Message objects
    public static class Builder {
        private String sender;
        private String receiver;
        private String metadata = ""; // Default value
        private String body = "";     // Default value

        public Builder setSender(String sender) {
            this.sender = sender;
            return this;
        }

        public Builder setReceiver(String receiver) {
            this.receiver = receiver;
            return this;
        }

        public Builder setMetadata(String metadata) {
            this.metadata = metadata;
            return this;
        }

        public Builder setBody(String body) {
            this.body = body;
            return this;
        }

        public Message build() {
            return new Message(sender, receiver, metadata, body);
        }
    }
}

// Usage
Message message = new Message.Builder()
    .setSender("Alice")
    .setReceiver("Bob")
    .setMetadata("RSA Encrypted")
    .setBody("Hello, Bob!")
    .build();
```
## Conclusion
The journey into design patterns has illuminated how these concepts can dramatically improve software design. By identifying and applying the factory method and builder patterns, I gained new insights into crafting scalable, maintainable solutions. While this exploration only scratches the surface, understanding design patterns equips me with tools to write more efficient, robust code in future projects—one step closer to becoming the best engineer I can be.
