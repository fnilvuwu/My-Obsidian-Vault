Questions represent the view of the situation before we take the next step and move on our way.
**The most important and most difficult thing in any situation is not the search for the right answer but the search for the right question.**
Copying and imitating what has been shown and explained will not always produce the desired result.

We can all ask questions. However, not many know how to ask the right questions. Because some significant differences and influences can greatly affect the answers we want to receive. The goal of the question is one of the most important aspects that determine our approach and the question we ask. Let us look at a few things that we currently use in our everyday lives. Such goals that we have just talked about can be, for example:
- To understand the reason for an event (`past`)
- To experience something completely new and to understand the way something works (`present`)
- to predict the effect of an event (`future`)

Every question is based on three aspects with which we build our questions every day:

1. origin
2. process
3. result/goal

## Relationship-Oriented-Questioning Model

![[Relationship-Oriented-Questioning Model.png]]

We need these components to be able to ask any question correctly. To do this, we ask any question we are interested in and break it down using the `ROQ` model. Certain aspects must be considered with this model, as with all others.

1. We need to find out the core element of the question and insert it as the object.
2. We must have at least two components defined in the model. More than two components are optional.

The good thing is that we always already have one component:

- Our position in the question.

Example of applying it :
- `What are all the methods available to remotely access Windows operating systems?`

![[Relationship-Oriented-Questioning Model - Windows as Object.png]]

Based on the parts assigned to the components, we now have to define in which relationship they act among each other. In the graphic, we see solid and dashed lines.

- `Solid line`: Connection - How is X connected to Y?
- `Dashed line`: Affection - How does Y influence the state of component X?

#### Connecting the Components

With this, we can go through the individual relationships and establish them between the individual components. It is recommended to always start with the object, which in this case is the Windows operating system. First, we need to establish and understand our position on the object.

- What is the purpose for us to use Windows?

Mainly we use the operating system to use its functions to solve our tasks. We describe this as `Operating on`.

- How does Windows influence our state in our position?

Windows is the most used operating system in the world and has the most compatibility and many user-friendly functions. Therefore, we can also summarize this and call it `Provides functionality`.
![[Relationship-Oriented-Questioning Model - Provides functionality.png]]

Now we can connect the relations between Windows and the methods we know.

- What must Windows do or offer to be managed by remote access methods?

A service must allow remote access over the Internet or network. We know for sure `WinRM`, `Remote Desktop`, and a few more. (If not, it does not matter. We will learn about these in other modules). Otherwise, we would not be able to access it remotely. We call this connection `Listening Service`.

Next, the following question comes up:

- How do the remote access methods affect Windows and thus change the state of Windows? What do these methods provide us with?

Here the answer and the purpose are already in the description - these allow `Remote Access`
![[Relationship-Oriented-Questioning Model - Remote access.png]]

Now let us look at what we know about the known remote access methods.

- What is the purpose of remote access methods?

The purpose is to be able to manage Windows in different ways remotely. So all we do with it is to use it. So, therefore, we call this connection `Using`.

- How do the different remote access methods that we know affect us?

Apart from the different services these methods are designed for, they all have one thing in common. They allow us to interact with Windows. Therefore we call this connection `Allow to interact with`.

![[Relationship-Oriented-Questioning Model - Interact.png]]

Since we already know some remote access methods, we know how they are connected to Windows. Before Windows can be accessed remotely, the corresponding service must be running.

- Which services must Windows have running to use methods unknown to us?

We can not know this because the methods are unknown to us. Therefore we name it like this: `???`

Now the same question arises again.

- How do the remote access methods affect Windows and thus change the state of Windows? What do these methods offer us?

The different methods offer different ways to access Windows. Because the purpose of the methods, in this case, has not changed. Therefore we call it again: `Remote Access`.

![[Relationship-Oriented-Questioning Model - Unknown method.png]]

Now that we know and understand the relationships between all the individual components, we know exactly what information we are missing and what we should focus on. In this case, we can use `Windows services` to find the unknown remote access methods. Therefore, if we look closely at all possible services that allow remote access, we can probably even find our own ways to use the service for remote access.

The special thing about this model is that it is stackable. For example, if we have identified such Windows services and found unknown methods, the field `Unknown` becomes `Known` and would look like this:

![[Relationship-Oriented-Questioning Model - Stackable.png]]

However, this model has one special feature. If applying this model to your question is unsuccessful, you will have to rephrase it and make it more precise. Because this feature of the `ROQ` model will not allow us to ask questions to which there is no clear answer.

Now, let us settle one last question.

- So, what is the right question?

`A right question is a precise question that allows us to establish the relationships between the components, to understand them, and to take us one step further to the required answer.`