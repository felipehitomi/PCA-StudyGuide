# Tracing and Spans

[https://medium.com/dzerolabs/observability-journey-understanding-logs-events-traces-and-spans-836524d63172](https://medium.com/dzerolabs/observability-journey-understanding-logs-events-traces-and-spans-836524d63172)

[https://docs.google.com/presentation/d/1GIvoN2nmXM9s2_7SJ2FWceDAG6XBvXTTTIo5FNfUNeQ/edit#slide=id.p](https://docs.google.com/presentation/d/1GIvoN2nmXM9s2_7SJ2FWceDAG6XBvXTTTIo5FNfUNeQ/edit#slide=id.p)

**Spans**

A Span represents a unit of work. They can be thought of as the work being done during an operation’s execution.

Logs
 represent occurrences at a specific point in time. Events aren’t that 
much more useful, other than being easier to read and query. The problem
 is that in isolation, Events don’t really tell a story. What if 
instead, we captured info for **a given block of time** (i.e. a time span)?

***************************************************************************************************************o Span conta uma historia sobre algo, ele “linka” eventos, então voce tem sempre um span como filho de outro, menos o primeiro que é o root.*************************************************************************************************************** 

Suppose we had the scenario below:

![https://miro.medium.com/max/700/1*L0TX12i3IISH9kjpjHfaLw.png](https://miro.medium.com/max/700/1*L0TX12i3IISH9kjpjHfaLw.png)

In the olden days, we’d have log that looked like this:

![https://miro.medium.com/max/700/1*-4K_INw4JN8MrCtdYdGgZg.png](https://miro.medium.com/max/700/1*-4K_INw4JN8MrCtdYdGgZg.png)

We have a span that looks like this:

![https://miro.medium.com/max/700/1*xYE9bueKrdhN04frG6u1kQ.png](https://miro.medium.com/max/700/1*xYE9bueKrdhN04frG6u1kQ.png)

In order for the Span to be more useful to us, we need some additional information. In OpenTelemetry, we can also include the following metadata in our Spans:

- **Operation name**: The name of the microservice being executed, or a function call
- **Start timestamp**
- **End timestamp** (or duration)
- **[Attributes](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/common/common.md#attributes):** (Optional) List of key-value pairs used for aggregation or for
filtering trace data (e.g. customer identifier, process hostname). Used
to describe and contextualize the work being done under a Span.
- **Events**: (Optional) Time-stamped strings which are made up timestamp, name, and
(optional) Attributes. Used to describe and contextualize the work being done under a Span.
- **Parent ID**: Unique identifier of the Span’s parent
- **[Links](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/overview.md#links-between-spans):** (Optional) References to other causally-related Spans

Now with the above metadata, we’ve got the proper context which helps us paint a picture of what happens during that operation.

***************************************só colocando as informações que temos ali encima não ajudaria muito, então é interessante colocar mais dados no span para que a busca e o entendimento sejá mais claro. Por exemplo quem executou pode te mostrar todo o caminho que foi seguido.*************************************** 

**Trace**

Traces are also known as distributed traces. They traverse network, process, and security boundaries, to give you a holistic view of your system.

A Span is the basic building block of a Trace. A Trace is made up of a tree of Spans, starting with a Root Span (i.e. Span with no parent), which encapsulates the end-to-end time that it takes to accomplish a task. The Root Span represents a single logical operation, such as clicking a button to add an item to a shopping cart.

***O trace é uma lista de ações que aconteceu com os spans, é uma “arvore” então temos a raiz que liga de começo a final.*** 

**Conclusion**

- Logs tell you about something at a particular point in time. They don’t have a standardized format, and are therefore hard to query.
- Events are structured logs (JSON), and are easier to query.
- Spans represent an operation. They paint a picture of what happened during
the time in which that operation was executed, through contextual
information such as associated Events and attributes.
- A Root Span is a Span without a parent, and represents your high-level
operation (e.g. clicking a button to add item to a shopping cart).
- Traces stitch all related spans (as a tree) together to tell you the whole story.