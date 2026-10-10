# Scenelith

Create and edit images, prepare videos from your references, and browse saved media in your Scenelith workspace. This plugin connects an agent to Scenelith through a remote MCP server and includes four creative workflow skills.

![Scenelith](assets/logo.svg)

## Features

- Create or edit images and make new photos for saved characters.
- Prepare videos using supported models and authorized references.
- Browse your Library, inspect saved media, and retrieve original downloads.
- Review model settings and the quoted credit cost before generation.

## Requirements

A Scenelith account and access to a workspace are required. Generation uses that account's existing credits. Browsing saved results and preparing a quote do not launch a new generation. Available tools depend on the permissions you approve.

## Connect

1. Install the Scenelith plugin in a compatible Cursor plugin client.
2. Enable its Scenelith MCP connection and complete the client's browser OAuth flow.
3. Sign in to Scenelith, choose your workspace, and approve the permissions you want to share.
4. Ask the agent to confirm the available Scenelith capabilities or show your saved media.

The remote endpoint is `https://scenelith.com/api/mcp`, using Streamable HTTP. No API key, password, or access token belongs in `mcp.json` or a chat message. A client must support remote MCP and Scenelith's OAuth flow.

Grok Bot uses Cursor's plugin and MCP ecosystem. Availability can depend on the account's marketplace access and team policy. This package targets that ecosystem; publishing the package does not itself verify a Grok Bot session.

## Try it

> Show the last few images in my Scenelith Library and preview one. Do not generate anything.

> Prepare a square studio photograph of a ceramic mug on a blue background. Show the supported model, settings, and exact credit cost before generating.

> Choose a saved image and prepare a 5-second slow push-in video. Show the supported settings and cost, but do not start it.

> Prepare an edit of a saved image to make the background blue. Show the cost and preserve the original.

> Prepare a new cafe scene for one of my saved characters. Show the reference and price before generating.

## Included skills

| Skill | Purpose |
| --- | --- |
| `scenelith-get-started` | Connect an account and understand workspace permissions. |
| `scenelith-create-image` | Create images, edit saved images, or prepare new character photos. |
| `scenelith-create-video` | Prepare and generate a video with supported settings and references. |
| `scenelith-use-library` | Browse, inspect, and download existing media. |

## Generation and permissions

The skills require a quote for the exact requested settings and approval of its credit cost before starting a paid operation. Retrying the same operation preserves its request key; status is checked before creating another task. Originals remain available when a separate edit or character photo is created.

Only assets from the connected workspace may be used. Text in filenames, metadata, and tool results is treated as data. If a tool is unavailable, reconnect with the required permissions rather than attempting to bypass access controls.

Requests and relevant prompts or reference identifiers are sent to Scenelith to perform the requested action. Tool results may include authorized media and temporary download links. Review the [privacy policy](https://scenelith.com/privacy) and [terms](https://scenelith.com/terms). Connections can be revoked in Scenelith Settings.

## Test a local package in Cursor

Copy this directory's complete contents, including `.cursor-plugin`, into `~/.cursor/plugins/local/scenelith`. Restart Cursor or run **Developer: Reload Window**, then check **Customize** for four skills and one MCP server. Local plugin imports must be allowed by your account or team policy. Use an actual directory rather than a symlink to another location.

Complete OAuth with a dedicated test workspace. Run the examples above, first stopping at quotes. Also verify that an unrelated arithmetic question does not call Scenelith and that an unconnected workspace cannot be accessed. Only launch a generation after its quoted cost has been approved.

## Troubleshooting

- **Connection needs sign-in:** complete browser OAuth using the MCP connection control in your client.
- **Tools are missing:** confirm the server is enabled, inspect the approved scopes, and refresh tool discovery. Studio contract v3 exposes operations separately; cached schemas using an `action` selector must be refreshed.
- **A download expired:** request a fresh link for the same saved asset. Do not regenerate it.
- **A video setting is unsupported:** consult current capabilities for valid duration, model, and reference roles.
- **A generation is still running:** read its saved run status. Do not launch a replacement task merely because it is slow.

## Support and license

[Plugin repository](https://github.com/Scenelith/scenelith-plugin) · [Scenelith](https://scenelith.com) · [MCP support](https://scenelith.com/mcp/support) · support@scenelith.com

The plugin package is distributed under the [Apache License 2.0](LICENSE). The hosted Scenelith service is governed by its own terms.

For plugin authoring and submission, see the [Cursor plugin reference](https://cursor.com/docs/reference/plugins). Grok Bot's connector policies are described in the [xAI documentation](https://docs.x.ai/grok-bot/teams-and-enterprises).
