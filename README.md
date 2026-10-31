# SendNow for Cursor

![SendNow](logo.png)

Secure document sharing, branded data rooms, access controls, and viewer engagement analytics through SendNow's hosted MCP service.

This repository contains public client configuration and documentation. The hosted server implementation and application secrets are not included.

## Connect

You need a SendNow account and an internet connection. Account plan and storage limits apply. Install this plugin from the Cursor Marketplace after approval, enable the SendNow MCP server, then complete the browser OAuth flow using your own SendNow account.

You can also configure the remote server manually in Cursor's MCP settings:

```json
{
  "mcpServers": {
    "sendnow": {
      "url": "https://share.sendnow.live/mcp"
    }
  }
}
```

The server advertises OAuth discovery, dynamic client registration, and PKCE. No shared API key or client secret is bundled. Client-specific authorization must complete before tools can access your account.

For local plugin testing, place the repository contents in `~/.cursor/plugins/local/sendnow`, reload Cursor, and inspect Customize. See [Cursor's plugin documentation](https://cursor.com/docs/plugins). This package has not yet been tested in an installed Cursor client.

## Capabilities

| Tools | Purpose |
| --- | --- |
| `get_account_profile`, `get_account_usage` | Inspect the connected account's plan, storage, usage, and limits. |
| `list_documents`, `get_document`, `update_document`, `delete_document` | Find and manage documents on your account. |
| `start_document_upload`, `upload_document_direct`, `finish_document_upload`, `request_document_upload`, `check_document_upload` | Upload documents or open a browser upload flow when attachments are unavailable. |
| `create_secure_link`, `list_links`, `update_link_security`, `revoke_link`, `delete_link` | Create and manage trackable sharing links and their security settings. |
| `get_document_analytics`, `list_link_viewers` | Inspect document engagement and viewers. |
| `create_microsite`, `update_microsite`, `list_microsites`, `get_microsite`, `delete_microsite`, `get_microsite_analytics` | Build and manage branded data rooms and review engagement. |

Security options include download restrictions, email verification, authorized-viewer lists, NDA gates, and link expiry, subject to account plan availability.

## Example prompts

- "Check my SendNow plan and storage usage."
- "Find my pitch deck and prepare a trackable link with downloads disabled."
- "Create a data room for these documents with email verification."
- "Show viewer engagement for my latest document."

Before sharing confidential files, review the intended recipients and access settings. A tool may create an externally accessible link. Revoking a link or deleting a document or data room can remove access; review client approval prompts before these actions.

## Data and privacy

Tool arguments, uploaded files, and requested settings are sent to the hosted SendNow service. Documents, sharing links, data rooms, and analytics belong to the connected account. Sharing controls determine who can access content. Do not include passwords or API credentials in prompts or public submission notes.

- [Website](https://sendnow.live)
- [Privacy policy](https://sendnow.live/privacy)
- [Terms](https://sendnow.live/terms)
- [Support](https://sendnow.live/support)

If authorization fails, reconnect and finish browser consent. If an upload or security option is refused, check the account plan and quota before retrying. If file attachments are unavailable, ask for the browser upload flow rather than encoding large files into the chat.

## License

The client configuration and documentation are MIT licensed. The SendNow logo is a brand asset; no trademark rights are granted. The hosted service is governed by SendNow's terms.
