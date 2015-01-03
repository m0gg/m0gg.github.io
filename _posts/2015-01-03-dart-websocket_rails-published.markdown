---
layout: post
title:  "Published dart-websocket_rails pub.dartlang.org"
date:   2015-01-03 23:36:00
categories: dart dart-rails websockets websocket_rails rails
---

[dart-websocket_rails](https://github.com/m0gg/dart-websocket_rails)
----------

Or in a pub-valid name `websocket_rails`. Again this is only special if you know about dart and rails. And obviously the [dart-rails](https://github.com/m0gg/dart-rails) gem.

If you've ever used websockets, you may know how handy the can be. Using websockets with the websocket_rails gem is very simple and convenient way if you're familiar with rails. This is one of the most recent projects created due to a private project i'm working on. It uses rails as well as AngularDart.

Now here comes something out of the current README of the master in [m0gg/dart-websocket_rails](https://github.com/m0gg/dart-websocket_rails)

Open a connection
-----------------

```ruby
WebSocketRails railsWs = new WebSocketRails('${window.location.host}/websocket')
  ..connect();
```

Subscribe to channel
----------------------

```ruby
Channel wsCh = railsWs.subscribe('foo');
```

Trigger an Event
----------------

```ruby
railsWs.trigger('music.is_votable');
railsWs.trigger('music.is_votable', { 'data': { 'bar_id': 1 }});
```

Trigger returns a `Future` which will be resolved when the websocket receives a response event.

```ruby
railsWs.trigger('music.is_votable', { 'data': { 'bar_id': 1 }})
  ..then((data) => print(data));
```

Bind to event
-----------------

`WebSocketRails` and `Channel` implement the internal `Binable` interface and thus can be bound the same ways. Currently there are two ways to bind to an event. But if you want to unbind a single event later, you'll need to choose the "dart-way".

"Old"-fashioned way

```ruby
wsCh.bind('bar', (data) {
  dyynamic m = JSON.decode(data);
  print(m);
});
```

"dart"-way

```ruby
StreamSubscription sc = wsCh.getEventStream('bar').listen((data) {
  dyynamic m = JSON.decode(data);
  print(m);
});
```

The `StreamSubscription` instance can later be `sc.cancel()`-ed to unbind a single event.


Summary
=======

Like it or don't, but i like it a lot. I'm still working on it, so if you're interested, keep checking back and make something awesome!
