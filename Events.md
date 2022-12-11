---
Tags: completed lec13
---
Links: [[EAD|HomePage]]
# Events
**Events** enable a class or object to *notify* other classes or objects when something of interest occurs. The class that *sends* (or raises) the event is called the *publisher* and the classes that *receive* (or handle) the event are called *subscribers*.

## Events Overview
- The *publisher* determines when an event is raised; the *subscribers* determine what action is taken in response to the event.
- An event can have multiple subscribers. A subscriber can handle *multiple events* from *multiple publishers.*
- Events that have no subscribers are *never raised.*
- Events are typically used to signal *user actions* such as button clicks or menu selections in graphical user interfaces.
- When an event has *multiple subscribers,* the event handlers are *invoked synchronously* when an event is raised.
-  In the .NET class library, events are based on the [EventHandler](https://learn.microsoft.com/en-us/dotnet/api/system.eventhandler) delegate and the [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/system.eventargs) base class.

#### How to Write Event Handler in C#?
In C#, an *event handler* is a method that responds to an event, such as a button click. Event handlers are usually registered with an event by adding the += operator after the event. For example:
`button1.Click += new EventHandler(button1_Click);`
When the button is clicked, the button1_Click method will be called.

<u>Step by Step Process of Writting Event and Event Handler in C#</u>
1. First, create an event by using the event keyword.
2. Next, create an event handler delegate that has the same signature as the event.
3. Finally, write the code for the event handler method.

```ad-caution
- The events in C# happen in a specific order
- The events in C# are triggered by various actions, such as user input, system events, or timer expiration
- The handlers for the events in C# can be written in either C# code or in Visual Basic code

```

##### Example-1

```cs
using System;

// Create Delegate
delegate void MyEventHandler();
delegate void MySecondEvent(object sender, string str);

class MyProgram
{

    // Publisher Class
    class MyButton
    {
        // 1. define events
        public event MyEventHandler click;
        public event MySecondEvent doubleclick;

        // 2. Raise event "On[EventName]"
        public void OnClick()
        {
            click();
        }

        public void OnDoubleClick()
        {
            doubleclick(this, "Double Clicked Saaaiqqee");
        }
    }
    
    // Subscriber/Listener Class
    class MyHandler
    {
        public void HandleEvent()
        {
            Console.WriteLine("Clicked Saaiiqqqe");
        }
    }

    static void Main()
    {
        MyButton button = new MyButton();
        MyHandler handler = new MyHandler();

        // Register Event against an action method
        button.click += handler.HandleEvent;
        button.click += () => {Console.WriteLine("Lambda Saaaiqqqe");};
        button.click += delegate () {Console.WriteLine("Anonymous Saaaiqee");};

        button.OnClick();

        button.doubleclick += (object obj,string str) => Console.WriteLine(obj + " Sent " + str);
        button.OnDoubleClick();
    }
}

```

##### Example-2
```cs
using System;
using System.Collections;

// Create Delegate
delegate void MyEventHandler(object obj);

class MyProgram
{
    // 1. Publisher Class
    class MyList : ArrayList
    {
        // 1. define Event
        public event MyEventHandler add;

        // 2. Raise Event
        public override int Add(object value)
        {
            add(value);
            return base.Add(value);
        }
    }

    static void Main()
    {
        MyList list = new MyList();
        list.add += (object obj) => Console.WriteLine(obj);

        list.Add(69);
        list.Add(39);
        list.Add(88);
    }
}
```

##### Example-3
```cs
using System;
using System.Collections;

// Create Delegate
delegate void MyEventHandler(object obj);

class MyProgram
{
    // 1. Publisher Class
    class MyList : Stack
    {
        // 1. define Event
        public event MyEventHandler push;
        public event MyEventHandler pop;

        // 2. Raise Event
        public override void Push(object value)
        {
            push(value);
            base.Push(value);
        }

        public override object Pop()
        {
            
            object obj = base.Pop();
            pop(obj);
            return obj;
        }
    }

    static void Main()
    {
        MyList list = new MyList();
        list.push += (object obj) => Console.WriteLine(obj + " pushed");
        list.pop += (object obj) => Console.WriteLine(obj + " poped");

        list.Push(69);
        list.Pop();
        list.Push(88);
    }
}
```

#### Example-4
```cs
using System;
using System.Collections;


class MyArgs : EventArgs
{
    public string name;
    public string message;
}

class MyProgram
{

    // Publisher Class
    class Publisher
    {
        // 1. Define Event
        public event EventHandler<MyArgs> speak;

        // 2. Raise Event
        public void Speak()
        {
            MyArgs args = new MyArgs{name = "Muhammad Ahmad", message = "Hey how you doing?"};
            speak?.Invoke(this, args);
        }

    }

    public static void Main()
    {
        Publisher speaker = new Publisher();
        speaker.speak += (Object sender,MyArgs args) => Console.WriteLine(args.name + ":" + args.message);
        speaker.Speak();
    }
}
```
---
> From wonder into wonder existence opens.
> — <cite>Laozi</cite>

Created: 2022-12-01