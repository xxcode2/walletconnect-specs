# Client API

```typescript
abstract class Client {
  // ---------- Methods ----------------------------------------------- //

  // initializes the client with persisted storage and a network connection
  public abstract init(): Promise<void>;

  // for responder to pair a pairing created by a proposer
  public abstract pair(params: { uri: string }): Promise<Sequence>;
 
  // request wallet authentication
  public abstract request(params: RequestParams): Promise<{ uri, id }>;

  // respond wallet authentication
  public abstract respond(params: RespondParams): Promise<boolean>;
  
  // query all pending requests
  public abstract getPendingRequests(): Promise<Record<number, PayloadParams>>;
  
  // query cached request matching id
  public abstract getRequest(params: { id: number }): Promise<ResponseParams>;
  
  // ---------- Events ----------------------------------------------- //

  // subscribe to auth response
  public abstract on("auth_response", (id: number, response: ResponseParams) => {}): void;

  // for wallet to listen on auth request
  public abstract on("auth_request", (id: number, payloadParams: PayloadParams) => {}): void;
}
```