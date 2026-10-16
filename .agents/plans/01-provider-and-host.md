# Provider abstraction and the offline host

Grill this before any code. Open questions at the bottom are the ones that change the design.

## What Rig is not

Rig does not embed Grok Build, Copilot agent mode, Codex, or Claude Code. Those products own a loop. Rig owns the loop. A provider is a model endpoint plus auth. Server-side tools on that endpoint stay off: no provider web search, no provider code execution, no provider MCP. A tool call is a Rig contract, executed here, and the result goes back as the next turn.

## The call

One interface, registered per provider.

```
list models
authenticate (oauth or key, per account, many accounts)
complete (stream): messages, tools, model -> tokens, tool calls, usage
```

The system calls that. A provider translates.

xAI is the Responses API at `api.x.ai/v1/responses`. That is the Grok model, not Grok Build. Build is the same model with Build's tools and Build's loop. We send our tools and we run them.

OpenAI is the Responses API. Anthropic is the Messages API. Copilot is the models endpoint a Copilot token already reaches. Each adapter maps Rig's tool schema to that API's tool schema and maps the stream back. No adapter implements an agent.

Cursor is not a provider. A Cursor account does not hand a third party a model endpoint. Cursor's own key feature points the other way: you paste a provider key into Cursor. Hitching Rig to Cursor's private API would be a terms problem and a break on every release. A user with a Cursor subscription uses the underlying provider login here.

Accounts are many. The picker is account, then model, limited to what that account's subscription returns.

## The loop

A turn is Rig's. Send the prompt and the tool list. Stream tokens to the session. On a tool call, run the contract, push the result, continue. The verifier from the first version gates done. A provider that returns a server-side tool call is a bug in the adapter, refused.

Compaction is Rig's. The plan, the dirty set, and the open findings stay outside the model context and are re-injected.

## Host, offline first

The first version has no remote control. The host is the machine with the checkout. The app, the agent process, and the language server are local.

The session bus is a Hub from day one, even with one peer. Local windows attach to it. A later remote window attaches to the same Hub over MinimalWebTransport, and a web head is another peer. Nothing in the first version binds a public port. The interface is the same, so remote is a bind, not a rewrite.

Dart already has MinimalWebTransport and Hub. That is the reason the shell stays Dart.

## UI

Flutter. One UI. Platform code where the platform demands it, the same split already used for communications.

Uno is a second UI stack and a second language, for no gain over Flutter on desktop. A WASM core with a Flutter shell adds a boundary the transport does not need, since the transport is already Dart. Revisit WASM only if a hot piece has to be shared with a non-Dart peer.

The editor is Monaco in a webview, with the language pack's language server behind it. File access on desktop Flutter is not the constraint. The constraint is the editor widget, and a webview clears it without leaving Flutter.

Windows stays the Linux host through WSLg, as already decided. The app is the Linux build.

## Open questions for the grill

1. Copilot's models endpoint is what VS Code uses. Is that an acceptable dependency, or does Copilot wait until GitHub ships a supported one?
2. OAuth per provider, or a key paste as the first cut, OAuth second?
3. Does the Hub live in the Flutter process for v1, or beside it as a small .NET service from the start?
