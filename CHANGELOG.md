# 0.9.0

## Breaking Changes

- #130, #132 the async client has been split into its own crate, async-nats

# 0.8.6

## Bug Fixes

- #126 Fix port signedness issue on ServerInfo which
  prevented connecting to servers on ports over i16::MAX.

# 0.8.5

## Improvements

- #125 Remove Sync requirement for the handler function
  passed to Subscription::with_handler.

# 0.8.4

## Bug Fixes

- #123 Fix regex error when parsing creds due to missing
  the `unicode-perl` feature flag on the regex crate.

# 0.8.3

## New Features

- Add `Options::client_cert()`.

# 0.8.2

## Bug Fixes

- Flush outstanding messages when `Connection` is dropped.
- Call callbacks configured by `Options`.
- Shutdown only when the last `Connection` is dropped.

# 0.8.1

## Improvements

- Remove `async-dup` dependency.
- Update dependencies, notably `nkeys` to v0.0.11.

## Bug Fixes

- Fix a bug due to which TLS authentication was not
  working.
- Shutdown the client thread when `Connection` is dropped.

# 0.8.0

## New Features

- Add `asynk::Message::respond()`.
- Add `Options::with_nkey()`.

## Improvements

- Update the `smol` dependency.

## Breaking Changes

- Remove `crossbeam-channel` from the public API.

# 0.7.4

## Improvements

* Remove the `MutexGuard` held across await points
  inside `cleanup_subscriptions()` to allow futures
  returned by async methods to implement `Send`.

# 0.7.3

## New Features

* Expose the `asynk` module with the async client API.

# 0.7.2

## Bug Fixes

* Implement `Subscription::close` and
  `Subscription::unsubscribe` correctly, which would
  previously do nothing.

# 0.7.1

## Bug Fixes

* Fix a deadlock in `Subscription` when concurrently
  receiving the next message and draining.

## Misc

* Add `--auth-token` flag to the `nats-box` example.

# 0.7.0

## New Features

* Support has been added for NATS Headers
  via the `Connection::publish_with_reply_or_headers`
  method.

## Breaking Changes

* The underlying TLS implementation has been switched
  from native-tls to rustls. The previously exported
  TLS functionality has been removed, and now you can
  supply certificates with the
  `Options::add_root_certificate` method.

# 0.6.0

## New Features

* An experimental async `Connection` is now available
  to adventurous explorers by calling
  `Options::connect_async`.

## Breaking Changes

* `ConnectionOptions` has been renamed `Options`.
* The minimum supported Rust version (MSRV) is now
  1.40.0.

# 0.5.0

## Breaking Changes

* #60 `ConnectionOptions` construction has been simplified,
  and the `with_user_pass`, `with_token`, and
  `with_credentials` methods have been changed to being
  constructors for the type, rather than producing
  intermediate states.

# 0.4.0

## New Features

* #57 The `drain` method has been added to the
  `Connection` and `Subscription` structs.

## Breaking Changes

* #36 `Connection::close` is now infallible and has no
  return value
* #36 The redundant `Subscription::close` has been
  removed. The same functionality exists in
  `Subscription::unsubscribe`.
* bumped the MSRV to 1.39.0 in anticipation of possible
  async support.

# 0.3.2

## Misc

* The minimum supported Rust version (MSRV) is now
  made explicit, and lowered to version 1.37.0 from
  1.42.0. Crate version 0.3.1 has been yanked due to
  it having silently broken older Rust versions than
  1.42.0.

# 0.3.1

## New Features

* #19 TLS support has been added.

# 0.3

## New Features

* #16 Implement reconnection logic.
* #16 Buffer outbound data when in a disconnected state.
* #16 Learn about new servers using the received INFO block.
* #16 Callback functions may be provided via the new
  `Options::set_disconnect_callback` and
  `Options::set_reconnect_callback` which will be executed
  when the connection to a server has been terminated
  or when a new connection has been established afterward.

## Breaking Changes

* #11 `Connection::new` has been renamed `Options::new`.
* #13 The various iterators have been replaced with concrete
  implementations: `Iter`, `IntoIter`, `TimeoutIter` which
  ensure that the backing `Subscription` is not closed
  while they are in use.