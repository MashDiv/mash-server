# MashServer

> Mash Server is a lightweight web framework designed to build efficient API servers. It achieves this by leveraging the power of uWebSockets.js, a high-performance WebSocket library for Node.js.

## Quick start

### Install with NPM

```
npm i @mashdiv/uws
```

## Documentation

- [Hello MashServer](#hello-mashdiv-uws)
- [Applying middleware](#applying-middleware)
- [Dynamic Routes](#dynamic-routes)
- [Query Parameter](#query-parameter)
- [Multipart upload](#multipart-upload)
- [cors](#applying-cors)
- [Handling 404 route](#handling-404-route)
- [Handling globle error](#handling-globle-error)

### Hello MashServer

```ts
const server = new MashServer();
const PORT = process.env.PORT || 8080;

app.get("/", (req, res) => {
  res.json({ hello: "MashServer" });
});

app.listen(8080, () => {
  console.log(`>started @${PORT}`);
});
```

### Applying middleware

```ts
app.use((req, res, next) => {
  console.log("Hello from middleware");
  next();
});
```

### Dynamic Routes

```ts
app.get("/post/:id", async (req, res) => {
  const { id } = req.getParams();
  return res.json({ id });
});
```

### Query Parameter

```ts
// ?page=2&limit=3
app.get("/post", async (req, res) => {
  const { page, limit } = req.query();
  return res.json({ page, limit });
});
```

### Multipart upload

```ts
app.post("/upload", async (req, res) => {
  const filesArray = await req.file();

  filesArray?.map((file: MultipartField) => {
    // do something magical
  });

  res.json({ status: true, msg: "file uploaded successfully", data: {} });
});
```

### cors

```ts
app.use((req, res, next) => {
  const origin = "https://example.com";
  res.writeHeader("Access-Control-Allow-Origin", origin);
  res.writeHeader("Access-Control-Allow-Methods", "GET, POST");
  next();
});
```

### Handling 404 route

```ts
app.notFound((req, res) => {
  res.status(404).end("Not found");
});
```

### Handling globle error

```ts
app.error((err, req, res) => {
  console.error(err);
  res.status(500).end("Internal server error");
});
```

## License

Licensed under [MIT License](LICENSE).
