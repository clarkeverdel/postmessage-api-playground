# PostMessage API Proof of Concept

This POC demonstrates secure cross-origin communication between a parent window and an embedded iframe using the postMessage API.

## Files

- `index.html` - Landing page with project overview
- `iframe-content.html` - Third-party page that sends messages (embed this in your app)
- `parent-demo.html` - Demo parent application that embeds the iframe
- `vercel.json` - Vercel deployment configuration

## Local Testing

1. Install dependencies (optional, for local server):

   ```bash
   npm install
   ```

2. Start local server:

   ```bash
   npm start
   ```

   Or use any static file server.

3. Open http://localhost:8080 in your browser

## Deploying to Vercel

1. Push this code to a GitHub repository

2. Go to https://vercel.com and sign in

3. Click "Add New Project"

4. Import your GitHub repository

5. Vercel will automatically detect the static site and deploy it

6. Your iframe content will be available at:
   ```
   https://your-project-name.vercel.app/iframe-content.html
   ```

## Integration in Your Application

Once deployed, update your application to embed the iframe:

```html
<iframe
  src="https://your-project-name.vercel.app/iframe-content.html"
  width="100%"
  height="600"
  frameborder="0"
>
</iframe>
```

Then listen for messages:

```javascript
window.addEventListener("message", (event) => {
  // Verify origin in production!
  if (event.origin !== "https://your-project-name.vercel.app") return;

  console.log("Received message:", event.data);
  // Handle different message types
});
```

## Security Notes

- Always verify `event.origin` in production
- Use specific origins instead of '\*' for `postMessage`
- Validate message data before processing
- Consider implementing a message schema/protocol

## Message Types Supported

- Simple text messages
- JSON data payloads
- User actions/events
- Navigation requests
- Status updates
- Error messages
- Authentication tokens
- Custom events
- Form submissions
- E-commerce actions (Add to Cart)
