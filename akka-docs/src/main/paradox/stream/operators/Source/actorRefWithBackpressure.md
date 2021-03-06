# Source.actorRefWithBackpressure

Materialize an `ActorRef`; sending messages to it will emit them on the stream. The source acknowledges reception after emitting a message, to provide back pressure from the source.

@ref[Source operators](../index.md#source-operators)

## Signature

@apidoc[Source.actorRefWithBackpressure](Source$) { scala="#actorRefWithBackpressure[T](ackMessage:Any,completionMatcher:PartialFunction[Any,akka.stream.CompletionStrategy],failureMatcher:PartialFunction[Any,Throwable]):akka.stream.scaladsl.Source[T,akka.actor.ActorRef]" java="#actorRefWithBackpressure(java.lang.Object,akka.japi.function.Function,akka.japi.function.Function)" }

## Description

Materialize an `ActorRef`, sending messages to it will emit them on the stream. The actor responds with the provided ack message
once the element could be emitted allowing for backpressure from the source. Sending another message before the previous one has been acknowledged will fail the stream.

## Examples

Scala
:  @@snip [actorRef.scala](/akka-docs/src/test/scala/docs/stream/operators/SourceOperators.scala) { #actorRefWithBackpressure }

Java
:  @@snip [actorRef.java](/akka-docs/src/test/java/jdocs/stream/operators/SourceDocExamples.java) { #actor-ref-imports #actorRefWithBackpressure }

## Reactive Streams semantics

@@@div { .callout }

**emits** when there is demand and there are messages in the buffer or a message is sent to the `ActorRef`

**completes** when the `ActorRef` is sent `akka.actor.Status.Success`

@@@
